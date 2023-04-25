# Creating your own Web-App based on a REST-Service

**Bitte beachten Sie unten die fettmarkierten Stellen an denen Sie Ihre Leistung dem Dozenten präsentieren sollen**

## Create Flask-App (Python-based)

* Create app.py with the following content:

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

**Zeigen Sie bitte Ihr Ergebnis bis ca. 60 Minuten nach Beginn der Übung dem Dozenten. (20% der Leistung)**
