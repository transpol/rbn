# Threads und Sockets - Fertigstellung der Chat-App

**Bitte denken Sie wieder daran, die erbrachte Leistung dem Dozenten zu präsentieren bevor Sie die Übung verlassen. Die bis zur Übung drei erhaltenen Punkte sollten aus Ihrm Moodle-Konto ersichtlich sein.**

## Technische Voraussetzungen
  
* Entweder Sie haben Java und Maven auf Ihrem Laptop und können damit auch REST-Services erstellen, oder Sie verwenden stattdessen Eclipse mit Java in der VM des HWR-VPools:
  1. Stellen Sie eine VPN-Verbindung her, hier der Link zur Einrichtung: https://www.it.hwr-berlin.de/anleitungen/vpn/
  2. VMware Horizon Player starten, kann auch hier heruntergeladen werden: https://customerconnect.vmware.com/en/downloads/info/slug/desktop_end_user_computing/vmware_horizon_clients/horizon_8
  3. Mit vpool.hwr-berlin.de verbinden (Nutzer und Pass wie bei bei der HWR-Anmeldung)
  4. VM WI Windows 10 DBK 2 starten, dort gibt es ein aktuelles Eclipse 23 mit Maven-Integration
* Um eine echte Verbindung mit anderen Chat-Clients herstellen zu können, sollten Sie sowieso eine VM des HWR V-Pools verwenden, damit Ihr Rechner mit eigener IP im Intranetz der HWR erreichbar ist.

## Erweitern Sie das Programm um eine Komponente für Nachrichten (50% der Leistung)

**Der Dozent wird auf seiner VM im HWR V-Pool eine ChatReceiver (auf Port 5001) bereitstellen, der eine ChatMessage annimmt und eine MessageResponse zurück sendet. Ebenso wird auf Port 5000 wieder ein ChatServer laufen,
der eine PeerInfo erwartet und eine RegistrationResponse zurück sendet, genau wie bei Übung 4. Die IP-Adresse wird in der Übung bekannt gegeben.**

1. Testen Sie den ChatClient gegen den ChatServer des Dozenten, wie in Übung 4. Die Klassen ChatClient, ChatServer, PeerInfo, und RegistrationResponse (mit Liste der PeerInfo) sind im ZIP-File für Übung 4 auf Moodle verfügbar.
2. Erstellen Sie eine Klasse ChatSender für das Senden einer Nachricht an den ChatReceiver des Dozenten, wie in Übung 4. Verwenden Sie dabei die Klassen MessageResponse und ChatMessage, die für Übung 4 ebenfalls auf Moodle verfügbar sind.
4. Erstellen Sie eine Klasse ChatReceiver für das Empfangen von Nachrichten auf Port 5001, analog zum vorherigen ChatServer. Testen Sie den ChatSender gegen Ihren eigenen ChatReceiver.
4. Für die Kommunikation zwischen ChatSender und ChatReceiver können Sie die Klassen MessageResponse und ChatMessage verwenden, die ebenfalls auf Moodle verfügbar sind. 

## Erweitern Sie den ChatSender zu einer richtigen ChatApp (50% der Leistung)

1. Die ChatApp soll es mehreren Teilnehmern ermöglichen, einen anderen Teilnehmer auszuwählen und dann mit diesem Teilnehmer in einen Dialog zu treten.
2. Neben einer Kommandozeilen-Lösung können Sie optional auch eine einfache GUI hinzufügen, so wie Sie es in OOP2 gelernt haben.

