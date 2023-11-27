# Working with Java Net

## Technische Voraussetzungen
  
1. Sie sollten Java installiert haben. Prüfen Sie die Version mit java -version. Version 17 wird von den Beispielen in der Übung teilweise verlangt.
  
2. Sie sollten Maven installiert haben oder Maven aus Ihrer IDE heraus aufrufen können. Eclipse wird vom Dozenten insbesondere unterstützt.

3. Es empfiehlt sich, auf der VPool-VM (an der HWR via Pool-PC) oder auf dem Pool-PC zu arbeiten und dort Maven auf dem H-Laufwerk zu installieren, da Sie sonst keine IP-Adresse im HWR-Netzwerk haben und daher auch die Übung nicht bearbeiten können.
     
## "Java Net" als normales Java Projekt ausführen

1. Legen Sie ein neues Java Projekt an.
2. Binden Sie die vier Klassen "Chat-Server-Registrierung" (Start Übung 4) ein.
3. Starten Sie den ChatServer.
4. Führen Sie den ChatClient aus. Schauen Sie sich die Ausgaben beider Programme an. 
5. Führen Sie den ChatClient erneut aus, ändern Sie aber vorher den Namen. Schauen Sie sich wieder die Ausgaben an.
6. Beenden Sie den ChatServer.

## Erweitern Sie das Programm um eine Komponente für Nachrichten

**Der Dozent wird auf seiner VM einen ChatReceiver bereitstellen, der eine ChatMessage annimmt und eine MessageResponse zurück sendet. Ebenso wird auf Port 5000 ein ChatServer laufen,
der eine PeerInfo erwartet und eine RegistrationResponse zurück sendet. Die IP-Adresse bzw. der Domainname sowie die Ports werden in der Übung bekannt gegeben.**

1. Testen Sie den ChatClient gegen den ChatServer des Dozenten.
2. Erstellen Sie eine Klasse ChatSender für das Senden einer Nachricht an den ChatReceiver des Dozenten. Verwenden Sie dabei die Klassen MessageResponse und ChatMessage, die ebenfalls auf Moodle verfügbar sind.
3. Erstellen Sie eine Klasse ChatReceiver für das Empfangen von Nachrichten auf Port 5001, analog zum vorherigen ChatServer. Testen Sie den ChatSender gegen Ihren eigenen ChatReceiver.

## Erweitern Sie den ChatSender zu einer richtigen ChatApp

1. Die ChatApp soll es mehreren Teilnehmern ermöglichen, einen anderen Teilnehmer auszuwählen und dann mit diesem Teilnehmer in einen Dialog zu treten.
2. Neben einer Kommandozeilen-Lösung können Sie optional auch eine einfache GUI hinzufügen, so wie Sie es in OOP2 gelernt haben.
