# Creating your own Web-App based on a REST-Service

**Bitte beachten Sie unten die fettmarkierten Stellen an denen Sie Ihre Leistung dem Dozenten präsentieren sollen**

## Create Flask-App (Python-based)

Create app.py with the following content:

```bash
from flask import Flask, render_template
import requests

app = Flask(__name__)

@app.route('/')
def home():
    response = requests.get('http://localhost:8080/greeting')
    todo = response.json()
    return render_template('index.html', todo=todo)

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```

This code defines a Flask application with a single route that consumes the REST API at localhost:8080 (Übung 2) and passes the returned JSON object to an HTML template called index.html.

This is the content of templates/index.html:

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

And this is the content of Dockerfile:
```bash
FROM python:3.8-slim-buster

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

Ahhh, wait, requirements.txt (for Python to work) is missing:

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

4. Make sure JAVA_HOME is set to the location of your JDK

5. Run "mvn --version" to verify that it is correctly installed.

For complete documentation, see https://maven.apache.org/download.html#Installation

Jetzt wird das Projekt aus Übung 2 (REST Service) gebaut:

1. Clone das Project aus Übung 2 (REST Service)
2. Importiere das Projekt (complete) in Eclipse als Maven-Projekt
3. Baue das Projekt mit 
```bash
mvn clean package
```
4. Danach befindet sich das fertig gebaute JAR-File im Verzeichnis *target*
5. Sie können es nun deployen, so wie in Übung 2. Dabei wird automatisch per Spring-Boot ein Tomcat-Server korrekt konfiguriert.

**Zeigen Sie bitte Ihr Ergebnis bis ca. 120 Minuten nach Beginn der Übung dem Dozenten. (80% der Leistung)**

## Create Own Spring-App

1. Initialize your project using the start.spring.io Website, make sure to include the Spring Web Dependency, chose Java as language, and Maven as Project.
2. Import your new project into Eclipse as Maven project (via pom.xml).
3. Create your own RestController class, e.g.
```bash
```
