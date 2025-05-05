# Die Evolution des Webs: Ein ausführlicher Sechs‑Phasen‑Überblick

Dieses Dokument erzählt die detaillierte Geschichte, wie aus isolierten Terminals und frühen Netzwerken das global vernetzte Web entstanden ist, das wir heute kennen. Wir betrachten den Übergang von Point‑to‑Point‑Verbindungen über dezentrale Diskussionsnetze und die Einführung von IP und DNS bis hin zu HTTP/HTML, der Verbreitung grafischer Browser sowie zu modernen, dynamischen und dezentralen Webdiensten.

---

## 1. 1969: ARPANET und der Beginn der Paketvermittlung

Vor ARPANET arbeiteten die meisten Rechner autark oder als Time‑Sharing‑Systeme in Großrechnerzentren. Anwender riefen mit Teletypen oder CRT‑Terminals über Modems eine zentrale Maschine an, wobei jeder Tastendruck als ASCII‑Zeichen übertragen wurde. Erste Versuche wie MITs CTSS oder das SAGE‑Luftverteidigungsnetz nutzten proprietäre Switches und eigene Protokolle, die eine Verbindung zwischen verschiedenen Systemen schwierig machten.

Um diese Isolation zu überwinden, finanzierte die US‑Verteidigungsforschungsagentur ARPA ARPANET. Entscheidende Neuerungen waren:

* **Dedizierte Leitungen und IMPs:** Anstelle von Direktverbindungen zwischen Hosts setzte ARPANET auf Interface Message Processors (IMPs) – robuste Minirechner an Standorten wie UCLA, Stanford und MIT –, die über 50 kbps‑Leitungen miteinander verbunden waren und das erste großflächige Paketvermittlungsnetz bildeten.
* **Paketbasierte Datenübertragung:** Hosts kommunizierten über eine standardisierte 1822‑Schnittstelle mit ihrem lokalen IMP. Nachrichten wurden in gleich große Pakete aufgeteilt, die hop‑by‑hop anhand dynamischer Routingtabellen weitergeleitet und am Ziel wieder zusammengesetzt wurden – ohne feste End‑zu‑End‑Leitungen.
* **Dienste als frühe Server:** Auf den Host‑Rechnern liefen Daemon‑Prozesse (z. B. Telnet für Remote‑Login, FTP für Dateiübertragung, erste Mail‑Protokolle), die auf definierten Ports auf Anfragen warteten und damit das Client‑Server‑Modell begründeten.

**IMPs als Router und Netzwerkkarten:** Durch die Auslagerung der Netzwerkschnittstelle in eigene Knoten wurden die Rechner von den physischen Verbindungsdetails entkoppelt, und die IMPs übernahmen gleichzeitig Aufgaben moderner Router und Network Interface Cards (NICs).

---

## 2. 1979: Usenet – Dezentraler Nachrichtenaustausch per UUCP

Parallel zu ARPANET entwickelten Tom Truscott und Jim Ellis ein leichtgewichtiges Diskussionssystem für UNIX‑Rechner: Usenet basierte auf UUCP:

* **Grundlagen von UUCP:** Das UNIX‑to‑UNIX Copy Program ermöglichte Datei‑ und Kommandoübergabe über serielle RS‑232‑Leitungen oder Modems. In Konfigurationsdateien (`/etc/uucp/Systems`, `Dialers`) waren Nachbarhosts, Telefonnummern und Anmeldeskripte hinterlegt.
* **Spool‑basiertes Versenden:** Anwender legten Beiträge in einem lokalen Spool‑Verzeichnis (`/var/spool/uucp`) ab. Ein nächtlicher Cron‑Job startete `uucico`, das die Modems per ATDT‑Befehl wählte, über eine Handshake‑Sequenz die Authentifizierung durchführte und neue Beiträge in Form von Rohdatenpaketen übertrug.
* **Verteiltes Store‑and‑Forward:** Das empfangende `uucico` schrieb Dateien in sein eigenes Spool. News‑Daemons (`inews`, `rnews`) verteilten die Artikel in hierarchische Newsgroups (z. B. `comp.lang.python`). Anschließend wurden weitere Nachbarn angerufen, bis jede Maschine alle neuen Beiträge erhalten hatte.
* **Hohe Ausfallsicherheit:** Ohne zentrale Instanz verbreiteten sich Beiträge auch bei einem Knotenausfall über alternative Routen. Ab Mitte der 1980er-Jahre erweiterte NNTP den Usenet‑Datenaustausch um Echtzeitübertragung über TCP/IP.

**Bezug zu ARPANET:** Ursprünglich lief Usenet vollständig getrennt vom paketvermittelten ARPANET. Erst durch Brücken zu TCP/IP‑Netzen verbanden viele Einrichtungen UUCP‑Verkehr mit dem Internet.

---

## 3. 1981: Einführung des Internet Protocol (IP)

Mit der wachsenden Zahl vernetzter Hosts wurde eine einheitliche Adressierung notwendig. In RFC 791 (September 1981) wurde IP:

* **32‑Bit‑Adressen:** Eindeutige numerische Adressen, unterteilt in Netzwerk‑ und Hostanteile. Adressklassen (A, B, C) ermöglichten unterschiedliche Netzgrößen.
* **Paketstruktur und Fragmentierung:** Header‑Felder für Version, Länge, Identifikation, Fragmentierung und Prüfsumme erlaubten das Durchqueren heterogener Netzwerke und das fehlerfreie Zusammensetzen von Fragmenten.
* **Vermittlung verschiedener Technologien:** IP stellte eine universelle Schicht dar, über die Ethernet, Satellitenverbindungen und das ARPANET zu einem frühen Internet zusammenwuchsen.

Vor IP pflegten Administratoren die zentrale Datei `HOSTS.TXT`, die Hostnamen zu IP‑Adressen zuordnete. Mit Tausenden von Einträgen wurde dieses manuelle Verfahren unpraktisch.

---

## 4. 1983: Skalierbarkeit durch DNS

Paul Mockapetris’ Domain Name System (RFC 882/883) löste das Namensproblem:

* **Hierarchisches Namensschema:** Wurzel, Top‑Level‑Domains (z. B. `.com`, `.edu`) und delegierte Subdomains erlaubten dezentrale Verwaltung.
* **Verteilte Delegation und Caching:** DNS‑Resolver fragten autoritative Server ab und speicherten Antworten im Cache, wodurch Latenz und Netzlast sanken.
* **Erstbetrieb:** Januar 1984 nahm SRI‑NIC (unter Jon Postel) die ersten Root‑ und TLD‑Server in Betrieb. Das Berkeley‑Paket BIND (Berkeley Internet Name Domain) mit dem Daemon `named` ersetzte sukzessive statische `/etc/hosts`‑Dateien.

**Abgrenzung zum Usenet‑Dial‑Up:** Telefon‑ und Anmeldedaten blieben in UUCP‑Konfigurationen; DNS lieferte nur Host‑zu‑IP‑Zuweisungen für TCP/IP.

---

## 5. 1989–1990: Tim Berners‑Lee und das World Wide Web

Am CERN erkannte Tim Berners‑Lee die Notwendigkeit eines universellen Hypertextsystems auf Basis von TCP/IP:

* **Uniform Resource Identifiers (URIs):** Eine allgemeine Syntax (`scheme://host[:port]/path`), um Dokumente weltweit eindeutig zu adressieren.
* **HTTP (HyperText Transfer Protocol):** Version 0.9 führte einfache `GET`‑Anfragen über TCP Port 80 ein und lieferte rohe HTML‑Texte zurück.
* **HTML (HyperText Markup Language):** Aufbauend auf SGML definierte HTML Tags wie `<a>`, `<p>`, `<img>` zur Strukturierung und Verlinkung von Dokumenten.

Die erste CERN‑Server‑Software httpd (1990) und der WorldWideWeb‑Browser auf NeXT‑Workstations verschmolzen Dokumenterstellung und -abruf in einem System, das Gopher und WAIS in Flexibilität und Erweiterbarkeit deutlich übertraf.

---

## 6. 1993–Heute: Von grafischen Browsern zu Web3

### 1993: NCSA Mosaic und der Durchbruch

Mosaic von Marc Andreessen und Eric Bina zeigte als erster Browser Bilder inline, bot eine benutzerfreundliche GUI und lief auf Windows, Mac und UNIX. Dies machte das Web für Laien zugänglich und leitete die Browser‑Kriege (Netscape vs. Internet Explorer) ein.

### Ende der 1990er–2000er: Dynamische Inhalte und Server‑Frameworks

* **CGI und eingebettete Skriptsprachen:** CGI‑Skripte (Perl, Python) generierten dynamische Seiten, litten jedoch unter hohem Overhead. In‑Prozess‑Module wie `mod_php`, `mod_perl` und `mod_python` sowie FastCGI reduzierten Latenz.

### 2010er–Heute: SPAs, Microservices und Cloud

* **JavaScript überall:** AJAX, Node.js und moderne Frameworks (React, Angular, Vue) ermöglichten responsive Single‑Page Applications.
* **API‑First und Microservices:** RESTful und GraphQL APIs, Containerisierung (Docker, Kubernetes) und Serverless-Architekturen optimierten Skalierbarkeit und Wartbarkeit.

### Aufkommendes Web3 und Dezentralisierung

* **Blockchain und DeFi:** Blockchain‑Netzwerke speichern Transaktionen in unveränderlichen Blöcken. Smart Contracts auf Plattformen wie Ethereum automatisieren Finanzprozesse ohne Zwischeninstanzen.
* **Dezentrale Protokolle:** IPFS, libp2p und dezentrale Identitätslösungen verfolgen das ursprüngliche Ideal der verteilten Zusammenarbeit weiter.

---

## 7. Moderne Schnittstellen und asynchrone Architektur

**WSGI vs. CGI:** WSGI (Web Server Gateway Interface) lädt Python‑Apps einmalig in den Serverprozess und ruft für jede Anfrage eine Callable‑Funktion auf, statt wie CGI einen neuen Prozess zu starten. Dies reduziert Latenz und Ressourcenverbrauch erheblich.

**ASGI vs. WSGI/CGI:** ASGI (Asynchronous Server Gateway Interface) erweitert WSGI um asynchrone I/O, WebSockets und Echtzeitkommunikation. Anwendungen implementieren `scope`, `receive` und `send` für hohe Parallelität und Multi‑Protokoll‑Support.

**AJAX:** Asynchronous JavaScript and XML nutzt JavaScript (`XMLHttpRequest` bzw. `fetch`) und DOM‑Manipulation, um Teilupdates einer Seite ohne kompletten Reload zu ermöglichen.

**Node.js:** JavaScript‑Runtime auf V8 mit ereignisgesteuertem, nicht-blockierendem I/O. Vereint Front‑ und Backend‑Entwicklung, befeuert durch das NPM‑Ökosystem.

**Blockchain und DeFi:** Blockchain verknüpft Blöcke kryptografisch und ermöglicht dezentrale Konsensmechanismen (Proof of Work/Stake). DeFi‑Protokolle implementieren Kasse, Handel und Kreditvergabe per Smart Contract, ohne zentrale Finanzdienstleister.

---

## Zusammenfassung

Diese Sechs‑Phasen‑Erzählung zeigt den Weg von isolierten Terminals und punktuellen Verbindungen über ARPANET und Usenet, die Einführung von IP und DNS, die Erfindung der Web‑Grundprotokolle durch Tim Berners‑Lee, den grafischen Browser‑Boom und den Übergang zu dynamischen, API‑basierten Diensten bis hin zu den ersten Experimenten im dezentralen Web3. Jeder Abschnitt baute auf den vorherigen Innovationen auf und führte zu größerer Skalierbarkeit, Benutzerfreundlichkeit und Offenheit – Merkmale, die das Internet zu der globalen Plattform gemacht haben, die wir heute nutzen.
