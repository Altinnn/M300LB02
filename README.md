# M300 - LB2

Diese Repository behandelt die Umsetzung von der LB2.

## Einleitung

Diese Dokumentation wurde von David Malic im Rahmen des Moduls M300 (Plattformübergreifende Dienste in ein Netzwerk integrieren)
erarbeitet und zeigt alle Schritte auf, die es braucht um die LB2-Kriterien zu erfüllen.

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
