# Creating your own Web-App based on a REST-Service

**Bitte beachten Sie unten die fettmarkierten Stellen an denen Sie Ihre Leistung dem Dozenten präsentieren sollen**

## Grundsätzliches

1. Jedes Docker-Projekt sollten Sie in einem eigenen Verzeichnis anlegen, möglichst unter <HOME>/docker. Verzeichnisnamen sollten dabei keine Leer- oder Sonderzeichen enthalten.
2. Jede Text-Datei enthält lediglich die angezeigten Zeichen und heißt genau so, wie jeweils angegeben. Um bei Windows und Mac sicher zu gehen, sollten Sie unbedingt die Dateien einzeln mit *more \<Dateiname\>* anzeigen lassen und mit *ls* bzw. *dir* die Verzeichnisse ausgeben lassen.

## Create Flask-App (Python-based, Docker-Projekt)

Legen Sie ein Verzeichnis für ein neues Docker-Projekt an. In diesem Verzeichnis: Create app.py (Text-Datei) with the following content:

```bash
from flask import Flask, render_template
import requests

app = Flask(__name__)

@app.route('/')
def home():
    response = requests.get('http://<IP-ADDRESS OF OWN MACHINE OR ubuntu22-001.lehre.hwr-berlin.de>:8080/greeting')
    todo = response.json()
    return render_template('index.html', todo=todo)

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```

This code defines a Flask application with a single route that consumes the REST API at *IP-Adresse:Port-Nummer* and passes the returned JSON object to an HTML template called index.html.

This is the content of templates/index.html (Text-Datei in Unterverzeichnis templates):

```bash
<!DOCTYPE html>
<html>
<head>
    <title>Flask Frontend</title>
</head>
<body>
    <h1>Todo</h1>
    <p>ID: {{ todo['id'] }}</p>
    <p>Content: {{ todo['content'] }}</p>
</body>
</html>
```

And this is the content of the Dockerfile (Text-Datei):
    
```bash
FROM python:3.8-slim-buster

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

Ahhh, wait, requirements.txt (Text-Datei, for Python to work) is missing:

```bash
Flask==2.0.2
requests==2.26.0
```

This can built like before ...

```bash
docker build -t flask-frontend .
```

Deploy ...
```bash
docker run -d -p 5000:5000 flask-frontend
```

Now open localhost:5000 (or any other host on which you have deployed).

**Zeigen Sie bitte Ihr Ergebnis bis ca. 60 Minuten nach Beginn der Übung dem Dozenten. (40% der Leistung)**

Hint: Later version of your flask-app may require you to iterate over an array of records returned by your app, in this case, the index.html needs to be modified:

```bash
    <ul>
        {% for item in todo %}
        <li>
            <p>ID: {{ item['id'] }}</p>
            <p>Content: {{ item['content'] }}</p>
        </li>
        {% endfor %}
    </ul>
```

## Installing Maven & Build Project (complete) from Übung 2
    
Download apache-maven-3.x.y ...   
    
1. Unpack the archive where you would like to store the binaries, e.g.:
   * Unix-based operating systems (Linux, Solaris and Mac OS X):
      tar zxvf apache-maven-3.x.y.tar.gz
   * Windows:
      unzip apache-maven-3.x.y.zip

2. A directory called "apache-maven-3.x.y" will be created. It might be good to have it under C:\Program Files\ on Windows.

3. Add the bin directory to your PATH, e.g.:

    * Unix-based operating systems (Linux, Solaris and Mac OS X):
      export PATH=/usr/local/apache-maven-3.x.y/bin:$PATH
    * Windows:
      set PATH="c:\program files\apache-maven-3.x.y\bin";%PATH%

4. Make sure JAVA_HOME is set to the location of your JDK, e.g. C:\Programme\Java\jdk-17 on Windows

5. Run "mvn -v" to verify that it is correctly installed. Double-check that "java -version" points to the same Version.

For complete documentation, see https://maven.apache.org/download.html#Installation

Jetzt wird das REST-Projekt aus Übung 1 - Aufgabe 2 gebaut, siehe https://spring.io/guides/gs/rest-service/:

1. Clone das Project: git clone https://github.com/spring-guides/gs-rest-service.git
2. Baue das Projekt gs-rest-service/complete mit 
```bash
mvn clean package
```
4. Danach befindet sich das fertig gebaute JAR-File im Verzeichnis *target*
5. Sie können es nun deployen, so wie in Übung 2. Dabei wird automatisch per Spring-Boot ein Tomcat-Server korrekt konfiguriert.

**Zeigen Sie bitte Ihr Ergebnis bis ca. 120 Minuten nach Beginn der Übung dem Dozenten. (80% der Leistung)**

## Create Own Spring-App

1. Initialize your project using the start.spring.io Website, make sure to include the Spring Web Dependency, chose Java as language, and Maven as Project.
2. Import your new project into Eclipse as Maven project (via pom.xml).
3. Create your own RestController.java, e.g.
```bash
import org.springframework.web.bind.annotation.RestController;

import java.util.ArrayList;
import java.util.List;

import org.springframework.web.bind.annotation.GetMapping;

@RestController
public class OurController {

    @GetMapping("/users")
    public List<User> getUsers() {
        List<User> users = new ArrayList<>();
        users.add(new User("John", "Doe"));
        users.add(new User("Jane", "Smith"));
        return users;
    }
}
```

using User.java as follows:

```bash
package rbn.demo.firstRBN;

public class User {
    private String firstName;
    private String lastName;

    public User(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
}
```
4. Build with mvn clean package
5. Create a Flask-frontend iterating over the users ...
6. Deploy everything in two docker containers ...

**Zeigen Sie bitte Ihr Ergebnis bis ca. 180 Minuten nach Beginn/ am Ende der Übung dem Dozenten. (100% der Leistung)**
