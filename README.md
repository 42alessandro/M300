# M300
Ebene mit einfachen Befehlen arbeiten.

Nachfolgend wird die VM mit einem bereits abgeänderten File bzw. VM aus dem M300-Repository erstellt:

Terminal (Bash) öffnen
In das M300-Verzeichnis (/M300/vagrant/web) wechseln:

  $ cd Pfad/zum-M300-Verzeichnis/vagrant/web
  
VM erstellen und starten:

  $ vagrant up
  
Webbrowser in der VM öffnen und prüfen, ob der Standard-Content des Webservers unter "http://10.4.32.:8080" erreichbar ist

Im Ordner /web die Hauptseite index.html editieren bzw. durch eine andere ersetzen (z.B. HTML5up-Themplate) und das Resultat überprüfen
Abschliessend kann die VM wieder gelöscht werden:
 
$ vagrant destroy -f


---
# Starten eines mariadb Server instanz und Status anzeigen
---Starten einer MariaDB instanz mit der neusten Version:
- $ docker run --detach --name some-mariadb --env MARIADB_USER=example-user --env MARIADB_PASSWORD=my_cool_secret --env MARIADB_ROOT_PASSWORD=my-secret-pw mariadb:latest
- Mit diesemm Befehl zeigt man die aktuell laufenden Containers an:
- $ docker stop ID (kann mit docker ps angezeigt werden)DANACH, um den Container wieder zu starten
- Mit diesemm Befehl zeigt man die aktuell gestoppten Containers an:
- $ docker ps -aHiermit löscht man einen vorhandenen Container
- $ docker rm (ID, kann mit docker ps angezeigt werden)---

# Ports und Netzwerkstatus
---Hiermit exportiert man den Port einer VM:
- $ docker run -p 80:80 -dnginxAktive Internet Status der Ports anzeigen:
- $ netstat -tulpn---

# Zugriff auf Containershell
---Hiermit erhaltet man Zugriff auf den laufendenden Container
- $ docker exec -it ID (kann mit docker ps angezeigt werden) "BEFEHL" (BSP: "/bin/bash" Verzeichnis gehen)Verlassen der Containershell
- $ exit---

# Löschen und wiederherstellen von Container / Volumes
---löschen von Container:
- $ docker rm ID (kann mit docker ps angezeigt werden)Auflisten der Volumes der erstellten Containers
- $ docker volume lsErstellen von Volumes
- $ docker volume create mydbstore(Name)Volumes werden auf der VM, auf der der Container läuft, lokale abgespeichert. Um den Pfad dieses Volumes auf der VM anzuzeigen hat man die Möglichkeit mit folgendem Command dies anzuschauen, beim folgendem Punkt: "Mountpoint":
- $ docker volume inspect mydbstore(name des Volumes)


# Supported tags und respective Dockerfile linksSimple Tags Beispiele:20.10.16, 20.10, 20, latest, 20.10.16-alpine3.16
20.10.16-dind, 20.10-dind, 20-dind, dind, 20.10.16-dind-alpine3.16
20.10.16-dind-rootless, 20.10-dind-rootless, 20-dind-rootless, dind-rootless
20.10.16-git, 20.10-git, 20-git, git
20.10.16-windowsservercore-ltsc2022, 20.10-windowsservercore-ltsc2022, 20-windowsservercore-ltsc2022, windowsservercore-ltsc2022
20.10.16-windowsservercore-1809, 20.10-windowsservercore-1809, 20-windowsservercore-1809, windowsservercore-1809

Docker bietet eine eingebaute Versionsverwaltung. Diese erlaubt es, den aktuellen Stand des Containers in ein Image zu sichern, dieses auf das Docker Hub zu laden, die Unterschiede zwischen dem aktuellen Zustand des Containers und dem ursprünglichen Image unterscheidet sich bei den Endungen. BSP: Version 20.10, ladet die neuste Version bsp: 20.10.12 herunter.Befehl, um die neuste Version herunterzuladen:
- $ docker pull "mariadb"Listet alle vorhandenen Images auf, welche isntalliert sind:
- $ docker image ls
- $ docker image list
- $ docker imagesMit diesem Befehl zeigt es die History des imagefiles an:
- $ docker image history (ID, kann mit docker image ls angezeigt werden)Mit diesem Befehl kann man das Imagefile inspizieren:
- $ docker image inspect (ID, kann mit docker image ls angezeigt werden)

# Container
Container verändern im Wesentlichen die Art und Weise, wie wir Pakete entwickeln, bereitstellen und ausführen.
Entwickler werden Pakete im eigenen Land erstellen, die mit dem gleichen Ansatz an anderen Orten ausgeführt werden können - egal ob es sich um ein Rack in der IT-Abteilung, den tragbaren Computer eines Benutzers oder einen Cluster in der Cloud handelt.
Administratoren können sich auf Netzwerke, Ressourcen und Zeit konzentrieren und müssen weniger Zeit für die Konfiguration von Umgebungen und die Bekämpfung von Systemabhängigkeiten aufwenden.

## Merkmale

- Container teilen sich Ressourcen mit dem Host-Betriebssystem
- Container können im Bruchteil einer Sekunde gestartet und gestoppt werden
- Anwendungen, die in Containern laufen, verursachen wenig bis gar keinen Overhead
- Container sind portierbar --> Fertig mit "Aber bei mir auf dem Rechner lief es doch!"
- Container sind leichtgewichtig, d.h. es können dutzende parallel betrieben werden.
- Container sind "Cloud-ready"!
# Docker

Um eine umfassende Lösung für die Erstellung und Verteilung von Containern zu entwickeln, hat Docker die bereits vorhandene Linux-Container-Technologie aufgegriffen und sie auf zahlreiche Arten verpackt und erweitert, vor allem durch portable Images und eine benutzerfreundliche Oberfläche. Die Docker-Plattform besteht aus zwei verschiedenen Teilen: dem Docker Hub, einem Cloud-Dienst zur gemeinsamen Nutzung von Container-Images, und der Docker Engine, die für die Erstellung und Ausführung von Containern zuständig ist.
Wichtig: Docker wurde für 64-bit Linux Systeme entwickelt, kann jedoch auch mittels VirtualBox auf Mac und Windows betrieben werden.

## Architektur
Die Hauptbestandteile von Docker sind im Folgenden aufgeführt:
### Docker Deamon
- Ausführen und Überwachen der Container, Erstellen
- Speichern und Bauen
Das Host-Betriebssystem startet normalerweise den Docker-Daemon.
### Docker Client
- Mittels des Docker Clients wird  Docker über die Kommandozeile (CLI) bedient
- Kommuniziert per HTTP REST mit dem Docker Daemon
- Mit dem Docker Daemon kommuniziert der Docker Client per HTTP Rest

Es ist einfach, sich mit entfernten Docker-Dämonen zu verbinden und Bindungen für Programmiersprachen zu erstellen, da die gesamte Kommunikation über HTTP erfolgt.

### Images
- Gebuildete Images sind Umgebungen, welche als Container gestartet werden können
- Images können nur neu gebuildet werden und sind nicht veränderbar
- Images bestehen aus Namen und Version (TAG), z.B. ubuntu:16.04.
- Wird keine Version angegeben wird automatisch :latest angefügt.

### Container
- Die ausgeführten Images sind Container
- Beliebig oft kann ein Image als Container ausgeführt werden
- Container bzw. deren Inhalte können verändert werden, dazu werden sogenannte Union File Systems verwendet, welche nur die Änderungen zum original Image speichern.

### Docker Registry
- Images werden in Docker Registries abgelegt und verteilt
Die Standardregistrierung ist Docker Hub, die sowohl "offizielle" Bilder als auch Tausende von öffentlich zugänglichen Bildern bietet.

Viele Organisationen und Unternehmen hosten kommerzielle oder "private" Fotos in ihren eigenen Registern, um die mit dem Herunterladen von Bildern aus dem Internet verbundenen Kosten zu vermeiden.

## Befehle
Die Anwendung kann mit einer Reihe von Befehlen verwendet werden, die vom Docker-Client bereitgestellt werden. Daher werden wir diese Befehle in diesem Abschnitt ausführlicher untersuchen.

### docker run
- Zum Starten neuer Container ist der Befehl.
- Der bei weitem komplexesten Befehl, er unterstützt eine lange Liste möglicher Argumente.
- Docker run Befehl ist bei weitem einer der komplexesten Befehl, er unterstützt eine sehr lange Liste an möglicher Argumente.
- Ermöglicht es dem Anwender, zu konfigurieren, wie das Image laufen soll, Dockerfile-Einstellungen zu überschreiben, Verbindungen zu konfigurieren und Berechtigungen  und Ressourcen für den Container zu setzen.
