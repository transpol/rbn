# First Steps with Docker

## Install Docker and/ or Login to your Project Docker VM

If you like to have Docker on your computer ...

* Install Docker Desktop
* Create a Login at Docker Hub (optional) and login with ...

```bash
docker login
```

Otherwise, simple ask your lecturer for the VM address and credentials. All group members will use a single account rbn on the same VM.

## Create a folder (Note, some commands on the host machine may have different syntax

Create a folder (mkdir = make directory) for the experiments and change (cd = change directory) into the folder:

```bash
mkdir docker
cd docker
```

## Check if Docker is running

Check if docker is installed. Enter in the command line (or power shell):

```bash
docker --version
```

Test docker:
```bash
docker run hello-world
```

More info about your Docker:
```bash
docker info
```

## Pulling an Image from Docker Hub (if you have an account)

If you have an account on Docker Hub ...

* Go to http://hub.docker.com/
* login to the website
* search for Ubuntu
* What is the last version of Ubuntu?

So let us pull it from Dock Hub to your computer, should even work without an account.

On you command line:
```bash
docker pull ubuntu
```

## List all Images

```bash
docker image ls
```

## List all Container

List all running containers:
```bash
docker container ls
```

List all containers:
```bash
docker container ls -a
```

## Running, stoping, and Attaching an Image

Starts Docker container and ends it right away:
```bash
docker run ubuntu
```

If you check the running containers, you see that there is no running container:
```bash
docker container ls
```

Starts Docker container and executes echo command:
```bash
docker run ubuntu echo "Hello BIPM"
```

Starts a Docker container and an interactive Bash. `-it` is short for `--interactive --tty` and will run it in the interactive mode:
```bash
docker run -it ubuntu bash
```

Some images have as a command line not Bash but a normal Shell `sh`. Normally you can always get the command line of a container.

You are now in the container and can interactively run commands:
```bash
pwd
```
```bash
ls
```
```bash
cd ~
```
```bash
ls
```
```bash
touch iwashere.txt
```
```bash
ls
```
To log out of the container, enter
```bash
exit
```

Now again the container is stopped.

If we login again,
```bash
docker run -it ubuntu bash
```
and go to your home directory
```bash
cd ~
```
check if the data is still there:
```bash
ls
```
The file is gone!

Check all containers.
```bash
docker container ls -a
```
```bash
CONTAINER ID        IMAGE                              COMMAND                  CREATED              STATUS                          PORTS               NAMES
a4cf0a5f41e7        ubuntu                             "bash"                   About a minute ago   Exited (0) 5 seconds ago                            objective_yonath
94cb0399ba60        ubuntu                             "bash"                   2 minutes ago        Exited (0) About a minute ago                       angry_goldstine
22863f7d24c0        ubuntu                             "bash"                   3 minutes ago        Exited (0) 3 minutes ago                            condescending_elgamal
```

The most right columnn you find `NAMES`. These names are automatically created. If we use the parameter `--name` we can name the container also by yourselfs.
You can also use the `CONTAINER ID` (first column) to identify a container  (e.g. a4cf0a5f41e7). There you do not have to write out the whole container ID but only use as many digits that are needed for identifying the container (normally two digits are sufficient)

Look not for the last but the the second last container (in this example `angry_goldstine` as NAME or `94cb0399ba60` as CONTAINER ID)

Restart the container (change the name or use the CONTAINER ID)
```bash
docker start angry_goldstine
```

Alternatively you could also use the CONTAINER ID (94cb0399ba60 in my case).
```bash
docker start 94cb0399ba60
```

You can als just use the first numbers of the CONATINER ID as long as they identify the container.
```bash
docker start 94
```

Login to an already running container with `docker exec` (change the CONTAINER ID);
```bash
docker exec -it 94 bash
```

`Ctrl+p` + `Ctrl+q` will turn the  interactive mode into a detached background (daemon) mode. That means you log out without stopping the container.

Check if the container is still running:
```bash
docker container ls
```

Login again. Alternatively to `docker exec -it` you can also use (change the CONTAINER ID)
```bash
docker attach 94
```

Go to your home directory
```bash
cd ~
```
check if the data is still there:
```bash
ls
```

The file is still here!

Use `Ctrl+p` + `Ctrl+q` to logout without stopping the container,

Check if the container is still running:
```bash
docker container ls
```

Stop the container if it is stil running (change 94cb0399ba60 to your container ID)
```bash
docker container stop 94cb0399ba60
```

Check if the container is still running:
```bash
docker container ls
```

## Deleting Containers

Check all containers:
```bash
docker container ls -a
```
Containers that you do not need anymore can be delete. This will delete all data on the container (change 94cb0399ba60 to your container ID)
```bash
docker container rm 94cb0399ba60
```

Check all containers:
```bash
docker container ls -a
```

You can delete all containers with
```bash
docker container prune
```
This is a dangerous command :-).

```bash
docker container ls -a
```
Everything gone.

## Containers and images

Let us start three different containers from the same image.
```bash
docker run -it -d --name ubuntu1 ubuntu bash
```
```bash
docker run -it -d --name ubuntu2 ubuntu bash
```
```bash
docker run -it -d --name ubuntu3 ubuntu bash
```

Meaning of the parameters:
* `--name` gives a container a name (e.g. ubuntu1)
* `-d` Detach: detaches the command line from the container so it is running in the background.


Check if all three containers running:
```bash
docker container ls
```

Start three more terminals, so that in total you have four terminals open.

In the second terminal, Enter
```bash
docker attach ubuntu1
```
In the third terminal, Enter
```bash
docker attach ubuntu2
```
In the fourth terminal, Enter
```bash
docker attach ubuntu3
```
In the termina of container ubuntu1 create a folder
```bash
mkdir iwashere
```
and check if it is there:
```bash
ls
```

In the termina of container ubuntu2 check if the folder `iwashere` is there:
```bash
ls
```

That means all containers are isolated.

Stop in the first terminal the ubuntu1 container.
```bash
docker container stop ubuntu1
```
What happens with your second terminal (where you are logged into ubuntu1)?

Stop all other containers.

## First Dockerfile - Start a simple website with nginx (Example first lecture)

Jetzt bauen wir unser erstes eigenes Docker image mit Hilfe eines Dockerfile (genau so benamt!) mit untigem Inhalt. Doch halt, erstmal legen wir ein Verzeichnis an für unser Projekt, z.B. simple_html und wechseln mit cd dorthin. Jetzt das Dockerfile:
```bash
FROM nginx:1.11-alpine
COPY index.html /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
Die erste Zeile ist das "base image", ein Linux-System mit dem Webserver nginx. Die Versionsnummer 1.11-alpine garantiert, dass unser Image stabil bleibt selbst wenn ein neueres nginx auf Docker Hub verfügbar wäre. In der zweiten Zeile kopieren wir eine eigene index.html (die wir erstellen) in den entsprechenden Pfad in unserem Docker container (der default Pfad von nginx für die anzubietenden Webseiten). In der dritten Zeile öffnen wir den Web-Port 80 nach außen. Und in der vierten und letzten Zeile starten wir den nginx als Dämon im Hintergrund.

Jetzt können wir unser Image bauen (mit dem Namen rbn-server):
```bash
docker build -t rbn-server .
```
Der Punkt am Schluß ist wichtig und gibt an, dass wir uns auf das aktuelle Verzeichnis beziehen, in dem sowohl die index.html als auch das Dockerfile liegen.

Jetzt können wir unseren Container schon starten ... doch Vorsicht, das erste 80 muss mit dem zugewiesenen Port ersetzt werden:
```bash
docker run -d -p 80:80 rbn-server
```
Hier steht das "-d" für "detached mode" und bedeutet soviel, als dass der Docker container im Hintergrund läuft. "-p 80:80" leitet den internen Port auf den äußeren Port 80 weiter. 

Nun 
```bash
<IP-oder-Web-Adresse>:<PORT-Nummer>
```
im Webbrowser aufrufen und das Resultat betrachten.

## Second Dockerfile - Create a simple REST Service with Java (JSON, Java, Maven, Spring Boot)

Um mit Java einen Rest Service to bauen und diesen per Spring zu deployen, sind folgende Schritte notwendig:
* Das Jar-File muss erstellt werden (mit Java, Spring Boot und Maven), folgen Sie hier bitte dem Tutorial https://spring.io/guides/gs/rest-service/
* Das Jar-File muss per Docker deployt werden
* Der REST-Service sollte getestet werden, folgen Sie hierzu wieder dem Tutorial

Hier ist das Dockerfile:
```bash
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY rest-service-complete-0.0.1-SNAPSHOT.jar /app
EXPOSE 8080
CMD ["java", "-jar", "rest-service-complete-0.0.1-SNAPSHOT.jar"]
```

Sollte es Ihnen nicht gelingen, das JAR innerhalb der Übung selbst zu bauen, so können Sie es auch aus dem Git-Repo hier entnehmen. Übrigens können Sie alles hier auch selbst herunter laden per
```bash
git clone https://github.com/transpol/rbn.git
```
