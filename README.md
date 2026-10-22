# Bachelorthesis: EPK-basiertes Ausführungsmodell für IoT-Systeme

**Entwicklung eines EPK-basierten Ausführungsmodells für die modellgetriebene Orchestrierung von IoT-Systemen auf Basis von CoAP**

Bachelor-Thesis von Amsakan Bavan im Studiengang Praktische Informatik an der Hochschule für Technik und Wirtschaft des Saarlandes (htw saar), angefertigt bei der SAG ARIS GmbH.

Betreuung und Begutachtung: Prof. Dr.-Ing. Steffen Knapp, Dr. Eric Wagner, Marc Lehmann, Niroshan Loganathan

## Worum es geht

Die Arbeit schließt die Lücke zwischen der Modellierung und der Ausführung von Geschäftsprozessen. Produktionsprozesse, die als Ereignisgesteuerte Prozesskette (EPK) in ARIS modelliert sind, werden von einem eigenen Compiler in eine ausführbare Form übersetzt und über CoAP auf IoT-Geräten ausgeführt.

Kernpunkte:

- formale Grundlagen aus Geschäftsprozessmodellierung, theoretischer Informatik (u. a. Kellerautomat) und eingebetteten Systemen
- Erweiterung der Prozessplattform ARIS um eine Execution-Engine und eine Automationsschnittstelle
- EPK-Compiler, der aus dem Prozessmodell Ausführungsknoten und CoAP-Pfade erzeugt
- Firmware für einen ESP32, der über I²C zwei Arduino-Modellanlagen ansteuert
- Rückführung der Ausführung als Ereignisprotokoll in ARIS Process Mining

Im Versuchsaufbau hält die Execution-Engine in allen Durchläufen den modellierten Pfad ein. Fünf der sechs definierten Anforderungen wurden erfüllt.

## PDF bauen

Voraussetzung ist eine aktuelle TeX-Live-Installation mit `latexmk`.

```sh
latexmk -pdf -interaction=nonstopmode -file-line-error htwsaar-i-mst-vorlage.tex
```

Das Ergebnis ist `htwsaar-i-mst-vorlage.pdf`. Das Literaturverzeichnis läuft über `biblatex` mit dem Backend `bibtex8`, `latexmk` ruft es automatisch auf.

Aufräumen der Hilfsdateien:

```sh
latexmk -c
```

### CI

Die GitLab-Pipeline (`.gitlab-ci.yml`) baut das PDF bei jedem Push und per Schedule im Container `ghcr.io/dante-ev/texlive:latest`. Das PDF liegt danach 30 Tage als Job-Artefakt bereit.

## Aufbau des Repos

```
.
├── htwsaar-i-mst-vorlage.tex   Hauptdokument (bindet alle Teile ein)
├── htwsaar-i-mst-config.tex    Pakete, Layout und Metadaten (Titel, Autor, Betreuer)
├── Bibliography.bib            Literaturdatenbank
├── Chapters/                   Inhaltskapitel und Anhang
├── FrontBackmatter/            Titelseite, Erklärung, Zusammenfassung, Verzeichnisse
├── Graphics/                   Abbildungen und draw.io-Quellen
├── network_latency.csv         Netzwerkmessungen aus den Validierungsläufen
└── Netzwerkmessungen.txt       zugehörige Roh-Logs der Execution-Engine
```

### Kapitel

1. Einleitung
2. Motivation und Zielsetzung
3. Grundlagen und theoretischer Rahmen
4. Related Work
5. Konzeption und Anforderungen
6. Systemdesign und Spezifikation
7. Technische Umsetzung
8. Ergebnisse
9. Fazit

Anhang A enthält UML-Diagramme, die Beispielprozesse und die Process-Mining-Auswertung.

### Abbildungen

Die Diagramme werden in [draw.io](https://www.drawio.com/) gepflegt (`Graphics/*.drawio`) und als PDF exportiert. Eingebunden werden nur die exportierten PDFs, PNGs und JPEGs. Nach einer Änderung an einer `.drawio`-Datei muss das PDF also neu exportiert werden.

### Messdaten

`network_latency.csv` enthält pro Durchlauf und Prozessschritt die Dauer von Health-Check und CoAP-Request in Millisekunden:

```
run,timestamp,executable_id,executable_name,request_type,target,duration_ms
```

`Netzwerkmessungen.txt` ist der dazugehörige Log-Auszug der Execution-Engine.

## Hinweise zum Ausdruck

Das Dokument ist für beidseitigen Druck gesetzt (`twoside,openright`) und sollte auch so gedruckt werden.

## Vorlage und Lizenz

Grundlage ist die LaTeX-Vorlage [htwsaar-i-mst-vorlage](https://github.com/systemtechniklabor/htwsaar-i-mst-vorlage) des Systemtechniklabors der htw saar.

Lizenziert unter der GNU General Public License v3.0 oder später, siehe [LICENSE](LICENSE).
