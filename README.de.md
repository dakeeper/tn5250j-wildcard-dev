# TN5250J

Ein 5250 Terminal-Emulator für IBM i (AS/400) in Java geschrieben.

[English](README.md) | [Deutsch](README.de.md)

Dieser Fork fügt Wildcard-Unterstützung für Gerätenamen hinzu:
- Verwende `*` oder `=` im Gerätenamen als Platzhalter für zufällige A-Z Zeichen
- Beispiel: `AA999BB*` wird zu `AA999BBA`, `AA999BBB`, etc. (zufällig)

Dokumentation verfügbar unter: [tn5250j.github.io](https://tn5250j.github.io/)

## Installation

### Voraussetzungen

- Java JDK 8 oder höher (nur JRE reicht nicht zum Bauen)
- ~500MB Festplattenspeicher für Abhängigkeiten

### Option 1: Bauen mit Ant (Empfohlen)

```bash
# Repository klonen
git clone https://github.com/dakeeper/tn5250j-wildcard-dev.git
cd tn5250j-wildcard-dev

# Projekt bauen
ant compile package

# Distribution mit allen Abhängigkeiten erstellen
ant dist-run-prepare
```

### Option 2: Bauen ohne Ant (Manuelle Kompilierung)

```bash
# Repository klonen
git clone https://github.com/dakeeper/tn5250j-wildcard-dev.git
cd tn5250j-wildcard-dev

# Build-Verzeichnis erstellen
mkdir -p build

# Java-Quellen kompilieren
javac -d build -source 1.8 -target 1.8 \
  -cp "lib/runtime/*" \
  -sourcepath src $(find src -name "*.java")

# JAR-Datei erstellen
cd build
jar cvfe tn5250j.jar org.tn5250j.My5250 $(find . -name "*.class")
cd ..

# Anwendung starten
java -jar build/tn5250j.jar
```

### Option 3: Fertiger Download

Lade die neueste JAR-Datei von der Releases-Seite herunter und starte sie:

```bash
java -jar tn5250j.jar
```

## Starten

Nach dem Bauen, starte die Anwendung:

```bash
# Mit kompiliertem JAR
java -jar build/tn5250j.jar

# Oder mit der Distribution mit allen Abhängigkeiten
java -jar dist/tn5250j-0.8.0-beta2-run/tn5250j.jar
```

## Konfiguration

Konfigurationsdateien werden in `~/.tn5250j` (Linux/macOS) oder `%USERPROFILE%\.tn5250j` (Windows) gespeichert.

### Konfigurationsdateien

| Datei | Beschreibung |
|------|-------------|
| `sessions.properties` | Sitzungskonfigurationen (Host, Gerätename, etc.) |
| `macros.properties` | Makro-Definitionen |
| `keymap.properties` | Benutzerdefinierte Tastenbelegungen |
| `TN5250JDefaults.props` | Standard-Einstellungen |

### Benutzerdefinierte Tastenbelegungen

Bearbeite `keymap.properties` in `~/.tn5250j`:

```properties
# Beispiel: Enter-Taste auf Rechte Strg-Taste ändern
Enter=10,true,false,false,false

# Tasten-Codes:
# 0=Nicht zugewiesen  9=TAB        10=Enter     27=Escape
# 37=Pfeil Links      38=Pfeil Hoch  39=Pfeil Rechts 40=Pfeil Runter
# 12=Clear            33=F1        34=F2        ... 48=F12
# 127=Löschen         155=Einfügen 157=Rechte Strg
# 150=Rechte Shift    151=Rechte Alt 152=Rechte GUI
```

### Makro-Definitionen

Bearbeite `macros.properties` in `~/.tn5250j`:

```properties
# Beispiel: Ein Makro erstellen, das "CALL MYPROGRAM" tippt
mac.1=type(CALL MYPROGRAM\r)
```

### Benutzerdefiniertes Einstellungsverzeichnis

```bash
java -Duser.home=/pfad/zu/einstellungen -jar build/tn5250j.jar
# oder
java -Demulator.settingsDirectory=/pfad/zu/einstellungen -jar build/tn5250j.jar
```

### Wildcard-Gerätenamen

Dieser Fork unterstützt Wildcard-Zeichen in Gerätenamen:
- Verwende `*` oder `=` als Platzhalter für zufällige A-Z Zeichen
- Beispiel: `AA999BB*` wird zu `AA999BBA`, `AA999BBB`, etc. (zufällig pro Verbindung)

## Unterstützte Plattformen

- Linux
- macOS
- Windows
- Jede Plattform mit Java 8+

## Lizenz

GPL-2.0

## Sicherheit

Dieser Fork wurde auf Sicherheitsprobleme geprüft. Der Code ist ein legitimer 5250 Terminal-Emulator für IBM i (AS/400).

### Sicherheitsprüfung

| Bereich | Status | Anmerkungen |
|---------|--------|-------------|
| Externe Befehle | OK | Nur für Browser-Öffnung und STRPCCMD (legitime IBM i Funktion) |
| Netzwerk/Sockets | OK | SSL/TLS für sichere IBM i Verbindungen |
| Passwort-Behandlung | OK | Passwörter werden nur im Speicher gehalten, nicht hardcodiert |
| SQL Injection | OK | JDBC verwendet parametrisierte Abfragen |
| Datei-Operationen | OK | Nur für Konfiguration und Export |
| Wildcard-Funktion | OK | Generiert nur zufällige A-Z Zeichen |

### Externe Exec-Verwendung

Der Code enthält legitime Verwendung von `Runtime.exec()`:
- **Browser starten**: Öffnet URLs im Standard-Browser
- **STRPCCMD**: IBM i Remote-Befehlsausführung (server-initiiert)
- **Spool-Export**: Derzeit auskommentiert

Dies ist Standard-Java-Funktionalität, die von vielen Anwendungen verwendet wird.

## Geschichte

Dieses Projekt wurde erstellt, weil es keinen Terminal-Emulator für Linux gab mit Funktionen wie fortgesetzte Edit-Felder, GUI-Fenster, Cursor-Progression-Felder, etc.

Es wurde dann Open Source gegeben, um etwas zurückzugeben an all die Hacker und Code-Entwickler, die so hart arbeiten, um die Linux- und Open-Source-Gemeinschaften mit qualitativ hochwertiger Arbeit und Software zu versorgen.

Der ursprüngliche Entwickler wollte, dass es auf verschiedenen Betriebssystemen funktioniert, daher das "J" für Java am Ende.

## Hosting

Das Projekt wurde zuvor bei [sourceforge.net](https://sourceforge.net/projects/tn5250j/) gehostet. Aber seit 2016 wurde es zu GitHub migriert.
