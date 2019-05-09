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

# K3 - Container
### Container

Es werden insgesamt 8 Container via `docker-compose.yml` aufgebaut:

| Container | Verwendung              |
| --------- | ----------------------- |
| `db-nc`   | Datenbank für Nextcloud |
| `app-nc`  | Nextcloud Applikation   |
| `web-nc`  | Webserver für Nextcloud |
| `app-pma` | phpMyAdmin              |
| `proxy`   | nginx-Reverse Proxy     |
| `certs`   | Self-signed Zertifikat  |

Es werden dabei keine Dockerfiles genutzt, stattdessen wird alles mittels `docker-compose` gelöst.

<br>

### Volumes

Damit die Daten beim stoppen nicht verloren gehen, werden mittel Volumes persistente Speicher erstellt:

| Volume                    | Nutzung                       |
| ------------------------- | ----------------------------- |
| `db-nc`                   | Speicher für die Nextcloud DB |
| `nextcloud`               | Nextcloud Daten               |
| `./web-nc/nginx.conf`     | nginx.conf für `web-nc`       |
| `certs`                   | Zertifikate                   |
| `./proxy/uploadsize.conf` | uploadsize.conf für `proxy`   |
| `vhost.d`                 | nginx-proxy Daten             |
| `html`                    | nginx-proxy Daten             |
| `/var/run/docker.sock`    | Docker-Daemon Socket (API)    |

<br>

#### Netzwerk

Da alle Container mit einem docker-compose.yml gebaut werden, können alle untereinander intern kommunizieren. Wird kein Port oder Netzwerk definiert, können die Container nicht nach aussen interagieren. Beispielsweise müssen alle Webserver (web-nc, app-wp, app-pma) das Netzwerk des Proxys und zusätzlich den "default"-Netzwerk haben, da sie ansonsten keine Verbindung aufbauen können.

<br>

### Schichtenmodell

[![M300lb2-Layer.jpg](https://i.postimg.cc/yYfqr81b/M300lb2-Layer.jpg)](https://postimg.cc/w7sb1HsX)

Das Schichtenmodell zeigt lediglich den Aufbau von _Docker für Windows_. Zu unterst die Infrastruktur/Hardware, danach ein Betriebssysten, Container Engine/Docker und darauf die Container.

<br>

### Umgebungsvariablen

Die Umgebungsvariablen werden entweder direkt im `docker-compose.yml` oder in einem `.env`-File definiert. \
Verwendete Umgebungsvariablen:

| Env-Variable          | Nutzende Container            | Beschreibung                                 |
| --------------------- | ----------------------------- | -------------------------------------------- |
| `MYSQL_ROOT_PASSWORD` | `db-nc`, `app-nc`, `db-wp`    | Root-Passwort für die MariaDB-Datenbank      |
| `MYSQL_PASSWORD`      | `db-nc`, `app-nc`, `db-wp`    | Passwort für den erstellten User             |
| `MYSQL_DATABASE`      | `db-nc`, `app-nc`, `db-wp`    | Zu erstellende Datenbank                     |
| `MYSQL_USER`          | `db-nc`, `app-nc`, `db-wp`    | Zu erstellender User                         |
| `VIRTUAL_HOST`        | `web-nc`, `app-wp`, `app-pma` | Hostname/(Sub-)Domain des Containers (Proxy) |
| `PMA_HOSTS`           | `app-pma`                     | Datenbanken für phpMyAdmin (Container Namen) |
| `SSL_SUBJECT`         | `certs`                       | Domain für das Zertifikat                    |
| `CA_SUBJECT`          | `certs`                       | Antragssteller                               |
| `SSL_KEY`             | `certs`                       | Speicherort .key-File                        |
| `SSL_CSR`             | `certs`                       | Speicherort .csr-File                        |
| `SSL_CERT`            | `certs`                       | Speicherort .crt-File                        |

<br>

### Testfälle

**Testfall 1: Websites aufrufen** 
Voraussetzungen: Container sind gestartet.

| Nr.  | Testfall                                   | Erwartet                                        | Effektiv                          |   OK   |
| :--: | ------------------------------------------ | ----------------------------------------------- | --------------------------------- | :----: |
| 1.1  | Nextcloud aufrufbar: <br>https://localhost | Seite wird geöffnet <br>Keine 500-Fehlermeldung | Seite wird ohne Probleme geöffnet | **OK** |
| 1.2  | phpMyAdmin aufrufbar: <br>http://localhost | Seite wird geöffnet <br>Keine 500-Fehlermeldung | Seite wird ohne Probleme geöffnet | **OK** |

**Testfall 2: Proxy** \
Voraussetzungen: Container sind gestartet.

| Nr.  | Testfall                                       | Erwartet                                                     | Effektiv                           |   OK   |
| :--: | ---------------------------------------------- | ------------------------------------------------------------ | ---------------------------------- | :----: |
|  2.  | Ports 80, 443 offen: <br>HTTP/S-Seite aufrufen | Seiten werden geöffnet <br>Keine Fehlermeldungen (ausser Zerti) | Seiten wird ohne Probleme geöffnet | **OK** |

# K4 - Sicherheit

## Service-Überwachung

Für die Container-Überwachung auf _Docker for Windows_ gibt es ein OpenSource-Tool, welches von der Community containisiert wurde: <https://github.com/maheshmahadevan/docker-monitoring-windows>. \
Es beinhaltet Prometheus (Backend) und Grafana (Frontend). Standardmässig gibt es zwei Dashboard: _Docker Host_ und _Docker Containers_. Darin werden bereits mehrere Ressourcen geloggt und grafisch dargestellt.

Zudem lassen sich damit auch Alarme einstellen, so dass bei einer vordefinierten Ereignis eine E-Mail, Slack-Benachrichtigung, etc. gesendet wird. 
Aber damit auch E-Mails versendet werden können, muss der SMTP-Server vorher in der `config.monitoring` definiert werden.

Sobald die Container gestartet sind, kann über <http://localhost:3000/> die Oberfläche aufgerufen werden. User und Passwort ist standardmässig `admin`. 
Anschliessend kann man beispielsweise einen Dashboard öffnen und dort die Auswertungen sehen. Zwar kann man diese über die Benutzeroberfläche bearbeiten, kann sie aber nicht abspeichern. Man muss entweder die Config (wird beim Speichern angezeigt) in die Zwischenablage kopieren, oder speichert es direkt als JSON-Datei ab. Diese Datei wird anschliessend in *./Monitoring/grafana/privisioning/dashboards* gespeichert. \
In meinem Beispiel habe ich ein neues Dashboard _Custom Dashboard.json_, welches auf _Docker Containers.json_ basiert. Ich habe lediglich noch einen Memory Usage-Panel hinzugefügt und daraus ein Alarm erstellt, sollte die Nutzung die 200MB überschreiten. \
**HINWEIS**: Damit die E-Mail versendet wird, muss im `config.monitoring` die SMTP-Daten angegeben werden. Ansonsten funktioniert es nicht.

Alle Dateien und Container befinden sich im Ordner Monitoring.

<br>

### Aktive Benachrichtigung

Wie bereits unter [Service-Überwachung](#Service-Überwachung) beschrieben, habe ich testweise einen Alarm erstellt, welches mir eine E-Mail sendet, sofern die Arbeitsspeicher-Auslastung die 200MB Grenze überschreitet (SMTP-Server muss vorher eingerichtet sein). \

Mit Grafana lässt aber noch viel mehr Benachrichtungen einstellen, wie z. B. Slack-Benachrichtigung, etc. Auch lassen sich diverse Alarme/Benachrichtungen einstellen.

<br>

### Container Absicherung

Um die Container selber abzusichern habe ich folgende Punkte erledigt:

- Non-Root User definiert*
- CPU-Nutzung begrenzt
- Arbeitsspeicher-Nutzung begrenzt
- Restart-Eingeschaft definiert (Was passiert wenn die Contianer sich selber ausschalten)

Der User kann entweder direkt im `docker-compose.yml` oder im Dockerfile definiert werden.

- docker-compose.yml --> `user: "Benutzer:Gruppe"` (siehe Beispiel)
- Dockerfile --> `USER Benutzer` (siehe Beispiel) 

CPU und Arbeitspeicher kann nur im `docker-compose.yml` begrenzt werden (oder direkt per Befehlszeile):

```
deploy:
  resources:
    limits:
      cpus: '0.25'
      memory: 256M
```

Die Restart-Eingeschaft wird im `docker-compose.yml` definiert. Es beschreibt, was passieren soll, sofern ein Container sich selber ausschaltet (sei es durch einen Befehl oder einen Absturz):
    

```
restart: <option>
```

Als `<option>` gibt es: `no`, `always`, `on-failure` oder `unless-stopped` \
Standardmässig verwendet man `always`, sofern der Container nicht von selbst ausgeschaltet werden soll.

<br>

#### Beispiele

- docker-compose.yml

  ```
  db-nc:
    image: mariadb
    container_name: nextcloud-mariadb
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    restart: always
    volumes:
      - db-nc:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=nextcloud
    env_file:
      - db-nc.env
    user: "mysql:mysql"
    deploy:
      resources:
        limits:
          cpus: '0.25'
          memory: 256M
  ```

- Dockerfile (_`USER appuser`_)

  ```
  FROM nextcloud:fpm-alpine
  
  RUN addgroup -g 2906 -S appuser && \
      adduser -u 2906 -S appuser -G appuser
  USER appuser
  ```

<br>

\* Es können nicht alle Container als Non-Root User ausgeführt werden, da diese Zugriff auf Systempfade benötigen (ansonsten erscheint die Fehlermeldung "Permission denied"). Möchte man sie dennoch als normalen User ausführen, müsste man solche Container komplett von Grund auf selber aufbauen. Was aus Zeitgründen in diesem Modul nicht möglich ist.


# K5

## Vergleich Vorwissen / Wissenszuwachs

Hauptsächlich konnte ich während dieses Projektes Fähigkeiten verbessern. Die Vagrant-Grundlagen habe ich bereits gekannt, konnte hier aber erstmals mit einem Multi-VM-System arbeiten. Allerdings habe ich zuvor noch nie Shell-Scripts für die automatisierte Installation von Diensten erstellt, was sehr lehrreich war.

Ich könnte während diesem Projekt sehr viel neues über Docker und insbesondere Kubernetes mit Google Cloud lernen, da ich zuvor erst mit Docker an sich gearbeitet habe. Deshalb habe ich mir in sehr vielen Gebieten neues Wissen zu Kubernetes aneignen können und auch ein paar neue Dinge bezüglich Docker gelernt.

## Reflexion

Ich habe zuvor noch nie mit Docker gearbeitet. Doch nach diesem Modul habe ich gesehen wie viel Docker mit sich bringt und wieviel zustanden kommen kann wen man diese auch beherscht. 
Ich würde mir in Zukunft mehr Zeit geben für das da ich mir nicht sicher bin ob ich alles gut gemacht habe und ob es so auch akzeptabel für einen genügende Note reicht.

## Vergleich Vorwissen/Wissenszuwachs
Vor den Projekt wuste ich noch nichts über docker sprich container usw. allerdings hatte ich diverse schwierigkeiten, die ich überwinden musste aber kann jetzt sagen, dass ich einigermassen docker gut verstehe. Der wissenszuwachs ist enorm. Wenn man bedenkt, dass ich vorher kein plan hatte und jetzt das einigermasesn in Griff habe ist es erstaunlich das alles für mich in dieser kurzen Zeit gelernt zu haben.

Ich hatte bisher noch nie mit Docker gearbeitet oder davon gehört, hatte zwar diverse schwierigkeiten doch mit einbisschen googlen und Youtube Videos ging das ganze schlussendlich doch gut aus.

Ich wusste nicht einmal wie man docker richtig konfigurieren muss und das mann in anfangs starten muss, auch Luafwerke spezifisch anhängen musste. Ich kannte die Befehle nicht usw.

## Kubernetes
Kubernetes fasst Container-Images, ihre Konfiguration und die Anzahl der benötigten Instanzen in Deployments zusammen, so der Sprachgebrauch des Orchestrierungssystems. Die Parameter eines Deployments überwacht Kubernetes selbsttätig. Das Tool sorgt dafür, dass die gewünschte Anzahl von Containern jederzeit läuft. Änderungen an der Software oder der Konfiguration verteilt Kubernetes mit einem Rollout. Dieser Prozess lässt sich pausieren, fortsetzen und rückgängig machen (Rollback).

Optimierung der Nutzung der Computer-Ressourcen Kubernetes setzt die Container eines Deployments selbständig dort ein, wo entsprechende Ressourcen frei sind. Der Anwender kann Mindest- und Höchstwerte der Ressourcennutzung (Rechenzeit, Speicherplatz) für die Container festlegen, um dem Orchestrierungstool einen Rahmen vorzugeben.

Zahlreiche Optionen für dauerhafte Datenspeicherung (Persistent Storage)

Container sind zustandslos. Für die dauerhafte Speicherung von Konfigurations- und Nutzerdaten bietet Kubernetes Schnittstellen zu zahlreichen Diensten wie zum Beispiel EBS von Amazon Web Services oder Google Cloud Platform.
