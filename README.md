# M300 - LB2

## Inhaltsverzeichnis

- K1
  - VirtualBox
  - Vagrant
  - Visualstudio-Code
- K2
  - Persönlicher Wissenstand
  - Wichtige Lernschritte sind dokumentiert
- K3
  - Bestehenden Docker-Dontainer kombinieren
  - Bestehende Container als Backend, Desktop-App als Frontend einsetzen
  - Volumes zur persistenten Datenablage eingerichtet
  - Kennt die Docker spezifischen Befehle
  - Eingerichtete Umgebung ist dokumentiert (Umgebungs-Variablen, Netzwerkplan gezeichnet, Schichtenmodell, Sicherheitsaspekte)
  - Funktionsweise getestet inkl. Dokumentation der Testfälle
  - Projekt mit Git und Mark Down dokumentiert
- K4
  - Service-Überwachung ist eingerichtet
  - Aktive Benachrichtigung ist eingerichtet
  - mind. 3 Aspekte der Container-Absicherung sind berücksichtigt
  - Sicherheitsmassnahmen sind dokumentiert (Bezug zur eingerichteten Umgebung ist vorhanden)
  - Projekt mit Git und Markdown dokumentiert
- K5
  - Vergleich Vorwissen - Wissenzuwachs
  - Reflexion
  - Vergleich Vorwissen/Wissenszuwachs
  - Kubernetes

------

# K1

## Virtualbox

Nun widmen wir uns der Virtualisierung von Computersystemen. Für den Betrieb von solchen Maschinen bzw. Computern stehen zahlreiche Virtualisierungsanwendungen zur Verfügung. Eine davon ist VirtualBox. In diesem Kapitel richten wir eine einfache VM (Virtuelle Maschine) mit VirtualBox ein. Also ganz traditionell und wie sich im späteren Verlauf zeigt, auch eine sehr aufwendige Arbeit.                                                     

## Vagrant

Vagrant sollte uns zeigen, dass das Bereitstellen virtueller Systeme in der konventionellen Art lange dauert und umständlich sein kann.
Abhilfe bietet hier Vagrant. Vagrant ist eine freie Ruby-Anwendung zur Erstellung und Verwaltung virtueller Maschinen und ermöglicht einfache Softwareverteilung.

## Visual Studio Code

Bis hierhin haben wir soweit alles aufgesetzt und installiert. Nun möchten wir für effizienteres Arbeiten eine "Entwicklungsumgebung" aufbauen, die es uns ermöglicht, alle lokalen Repositories an einem Ort zu verwalten und die dazugehörigen Dateien zu bearbeiten. Die Lösung hierzu ist: Visual Studio Code 
Dieser freie Quelltext-Editor von Microsoft, ermöglicht uns, unsere Workflows besser zu gestalten und damit die Arbeit um einiges leichter zu machen.

# K2

## Persönlicher Wissenstand

- Docker / Container:
  Ich habe zwar schon von Docker und Containern gehört mich aber leider nie mit diesem Thema befasst.
- Microservices: 
  Von Microservices habe ich ebenfalls schon öfters gehört und kenne es nur ein bisschen aus der Theorie. In der Praxis habe ich es nie angewandt und kenne mich deswegen auch nicht sehr gut aus.

# K2

## Kennt die Docker spezifischen Befehle

| Befehl       | Beschreibung                                       |
| ------------ | -------------------------------------------------- |
| docker run   | Führt ein Befehl in einem neuen Container aus      |
| docker start | Startet einen oder mehrere gestoppte Container     |
| docker stop  | Stoppt einen oder mehrere laufende ontainer        |
| docker build | Erstellt ein Image aus einem Docker-File           |
| docker pull  | Ladet ein Image aus der Registry                   |
| docker push  | Ladet ein Image in die Registry hoch               |
| docker exec  | Führ einen Befehl in einem laufenden Container aus |

| docker ps | Überblick über die aktuellen Container, wie z.B. Namen, IDs und Status
| docker images | Liste lokaler Images aus, wobei Informationen zu Repository-Namen, Tag-Namen und Grösse enthalten sind
| docker rm | Entfernt einen oder mehrere Container. Gibt die Namen oder IDs erfolgreich gelöschter Container zurück

# K5

## Vergleich Vorwissen / Wissenszuwachs

Hauptsächlich konnte ich während dieses Projektes Fähigkeiten verbessern. Die Vagrant-Grundlagen habe ich bereits gekannt, konnte hier aber erstmals mit einem Multi-VM-System arbeiten. Allerdings habe ich zuvor noch nie Shell-Scripts für die automatisierte Installation von Diensten erstellt, was sehr lehrreich war.

Ich könnte während diesem Projekt sehr viel neues über Docker und insbesondere Kubernetes mit Google Cloud lernen, da ich zuvor erst mit Docker an sich gearbeitet habe. Deshalb habe ich mir in sehr vielen Gebieten neues Wissen zu Kubernetes aneignen können und auch ein paar neue Dinge bezüglich Docker gelernt.

## Reflexion

Dieses Projekt war sehr lehrreich. Ich hatte gegen den Schluss ein bisschen Zeitdruck da ich die Zeit nicht optimal geplant habe. Mit dem Endresultat bin ich aber trotzdem zufrieden. Ich habe auch gemerkt wie wichtig Docker ist und das es bestimmt in Zukunft noch viel wichter sein wird. 

## Vergleich Vorwissen/Wissenszuwachs
Vor den Projekt wuste ich noch nichts über docker sprich container usw. allerdings hatte ich diverse schwierigkeiten, die ich überwinden musste aber kann jetzt sagen, dass ich einigermassen docker gut verstehe. Der wissenszuwachs ist enorm. Wenn man bedenkt, dass ich vorher kein plan hatte und jetzt das einigermasesn in Griff habe ist es erstaunlich das alles für mich in dieser kurzen Zeit gelernt zu haben.

Ich hatte bisher noch nie mit Docker gearbeitet oder davon gehört, hatte zwar diverse schwierigkeiten doch mit einbisschen googlen und youtube Videos ging das ganze schlussendlich doch gut aus.

Ich wusste nicht einmal wie man docker richtig konfigurieren muss und das mann in anfangs starten muss, auch Luafwerke spezifisch anhängen musste. Ich kannte die Befehle nicht usw.

## Kubernetes
Kubernetes fasst Container-Images, ihre Konfiguration und die Anzahl der benötigten Instanzen in Deployments zusammen, so der Sprachgebrauch des Orchestrierungssystems. Die Parameter eines Deployments überwacht Kubernetes selbsttätig. Das Tool sorgt dafür, dass die gewünschte Anzahl von Containern jederzeit läuft. Änderungen an der Software oder der Konfiguration verteilt Kubernetes mit einem Rollout. Dieser Prozess lässt sich pausieren, fortsetzen und rückgängig machen (Rollback).

Optimierung der Nutzung der Computer-Ressourcen Kubernetes setzt die Container eines Deployments selbständig dort ein, wo entsprechende Ressourcen frei sind. Der Anwender kann Mindest- und Höchstwerte der Ressourcennutzung (Rechenzeit, Speicherplatz) für die Container festlegen, um dem Orchestrierungstool einen Rahmen vorzugeben.

Zahlreiche Optionen für dauerhafte Datenspeicherung (Persistent Storage)

Container sind zustandslos. Für die dauerhafte Speicherung von Konfigurations- und Nutzerdaten bietet Kubernetes Schnittstellen zu zahlreichen Diensten wie zum Beispiel EBS von Amazon Web Services oder Google Cloud Platform.
