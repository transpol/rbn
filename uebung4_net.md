# Working with Java Net

**Bitte denken Sie wieder daran, die erbrachte Leistung dem Dozenten zu präsentieren bevor Sie die Übung verlassen. Die bisher erhaltenen Punkte sollten aus Ihrm Moodle-Konto ersichtlich sein.**

## Technische Voraussetzungen
  
1. Sie sollten Java installiert haben. Prüfen Sie die Version mit java -version. Version 17 wird von den Beispielen in der Übung teilweise verlangt.
  
2. Nur für die Musterlösung zu Übung 3 - Aufgabe 4 (und nur wenn Sie sie neu bauen wollen) sollten Sie auch Maven installiert haben oder Maven aus Ihrer IDE heraus aufrufen können. Eclipse wird vom Dozenten insbesondere unterstützt. Sind Sie technisch versiert, so können Sie auch eine andere IDE
  oder ein andere Build-Tool wie z.B. Gradle benutzen!
  
## Musterlösung Übung 3 - Aufgabe 4 anschauen

1. Laden Sie sich die Musterlösung von Moodle herunter und entpacken Sie diese.
2. Platzieren Sie den Ordner Newscrawler direkt in Ihrem eclipse-workspace.
3. Importieren Sie den Folder als Projekt in den Workspace. Da sich das Projekt physisch schon dort befindet, brauchen Sie es natürlich nicht mehr zu kopieren.
4. Bauen Sie das Projekt entweder aus Eclipse heraus (als Run Configuration mit den Zielen "clean package") oder direkt auf der Konsole mit mvn clean package
5. Sie brauchen das Projekt nicht in einem Docker-Container zu deployen, sondern können es auch direkt mit "java -jar target\newsCrawler-0.0.1-SNAPSHOT.jar" starten. 
   Das Ergebnis können Sie dann auf "localhost:8080/news" ansehen.
   
## "Java Net" als normales Java Projekt ausführen

1. Legen Sie ein neues Java Projekt an.
2. Binden Sie die vier Klassen "Chat-Server-Registrierung" (Start Übung 4) ein.
3. Starten Sie den ChatServer.
4. Führen Sie den ChatClient aus. Schauen Sie sich die Ausgaben beider Programme an. 
5. Führen Sie den ChatClient erneut aus, ändern Sie aber vorher den Namen. Schauen Sie sich wieder die Ausgaben an.
6. Beenden Sie den ChatServer.

## Erweitern Sie das Programm um eine Komponente für Nachrichten (50% der Leistung)

1. Erstellen Sie eine Klasse ChatReceiver für das Empfangen von Nachrichten auf Port 5001, analog zum vorherigen ChatServer.
2. Erstellen Sie eine Klasse ChatSender für das Senden von Nachrichten an alle Peers (die zuvor mit ChatClient abgefragt wurden).
3. Für die Kommunikation zwischen ChatSender und ChatReceiver können Sie die Klassen MessageResponse und ChatMessage verwenden, die ebenfalls auf Moodle verfügbar sind. 
4. Wenn Sie diese Klassen verwenden, können Sie den ChatSender auch gegen einen Beispiels-ChatReceiver testen, der vorraussichtlich auf ubuntu22-001.lehre.hwr-berlin.de:5001 vom Dozenten deployt wird.
5. Übrigens können Sie - falls Sie von einer VM des vpool aus Arbeiten - auch den ChatServer des Dozenten verwenden, der voraussichtlich unter ubuntu22-001.lehre.hwr-berlin.de:5000 deployt sein wird.
6. Sie müssen auf einer VM des VPool arbeiten, weil Sie sonst innerhalb des HWR-Netzes nicht unter einer festen IP erreichbar sein werden und daher keine echte Kommunikation zwischen den Kommilitonen möglich sein würde.

## Erweitern Sie den ChatSender zu einer richtigen ChatApp

1. Die ChatApp soll es mehreren Teilnehmern ermöglichen, einen anderen Teilnehmer auszuwählen und dann mit diesem Teilnehmer in einen Dialog zu treten.
2. Neben einer Kommandozeilen-Lösung können Sie optional auch eine einfache GUI hinzufügen, so wie Sie es in OOP2 gelernt haben.
