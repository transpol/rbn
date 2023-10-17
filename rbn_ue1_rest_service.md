# RBN - Uebung 1 - Creating your own REST-Service

**Falls diese Übung im Moodle-Kurs für heute verlinkt ist, können Sie damit 2% der Präsentationsleistung erbringen. Dazu müssen Sie 
dem Dozenten eine der unten vorgestellten Aufgaben präsentieren und frühestens nach 70% der Übungszeit eine Bestätigung verlangen. Bitte nutzen Sie die verbleibende 
Übungszeit (nach Bestätigung oder auch schon davor nach Fertigstellung der Übung) unbedingt um Ihr Projekt weiter zu entwickeln.**

## Decide where to deploy

1. Own Personal Computer: Install Java, Eclipse, and Maven (see below)
2. On VM: Connect from Pool PC with VMWare Horizon Client (vpool.hwr-berlin.de, Moodle Credentials) and deploy Maven on H: ... Java and Eclipse exist

Either way: Check with java -version and mvn -v

Use a startup.bat ...
```bash
set JAVA_HOME=C:\Program Files\Java\jdk-17
set Path=%JAVA_HOME%\bin;%Path%
set Path=H:\apache-maven-3.9.2\bin;%Path%
```

## Installing Maven & Build Project
    
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

1. Clone das Project: git clone https://github.com/spring-guides/gs-rest-service.git (Hinweis: Falls Sie kein Git haben, beispielsweise weil Sie auf einer VM arbeiten, können Sie auch das ganze Projekt als ZIP-Datei herunterladen)
2. Baue das Projekt gs-rest-service/complete mit 
```bash
mvn clean package
```
4. Danach befindet sich das fertig gebaute JAR-File im Verzeichnis *target*
5. Sie können es nun deployen, so wie in Übung 2. Dabei wird automatisch per Spring-Boot ein Tomcat-Server korrekt konfiguriert.

**Präsentieren Sie bitte Ihr Ergebnis dem Dozenten.**

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
