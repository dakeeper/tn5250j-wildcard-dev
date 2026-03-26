# TN5250J

A 5250 terminal emulator for the IBM i (AS/400) written in Java.

This fork adds wildcard support for device names:
- Use `*` or `=` in device name as placeholder for random A-Z character
- Example: `AA999BB*` becomes `AA999BBA`, `AA999BBB`, etc. (random)

Documentation is available at: [tn5250j.github.io](https://tn5250j.github.io/)

[![Build Status](https://travis-ci.org/tn5250j/tn5250j.svg?branch=travis)](https://travis-ci.org/tn5250j/tn5250j)

## Installation

### Prerequisites

- Java JDK 8 or higher (JRE only is not sufficient for building)
- ~500MB disk space for dependencies

### Option 1: Build with Ant (Recommended)

```bash
# Clone the repository
git clone https://github.com/dakeeper/tn5250j-wildcard-dev.git
cd tn5250j-wildcard-dev

# Build the project
ant compile package

# Create distribution with all dependencies
ant dist-run-prepare
```

### Option 2: Build without Ant (Manual Compilation)

```bash
# Clone the repository
git clone https://github.com/dakeeper/tn5250j-wildcard-dev.git
cd tn5250j-wildcard-dev

# Create build directory
mkdir -p build

# Compile Java sources
javac -d build -source 1.8 -target 1.8 \
  -cp "lib/runtime/*" \
  -sourcepath src $(find src -name "*.java")

# Create JAR file
cd build
jar cvfe tn5250j.jar org.tn5250j.My5250 $(find . -name "*.class")
cd ..

# Run the application
java -jar build/tn5250j.jar
```

### Option 3: Pre-built Download

Download the latest release JAR from the releases page and run:

```bash
java -jar tn5250j.jar
```

## Running

After building, run the application:

```bash
# Using the compiled JAR
java -jar build/tn5250j.jar

# Or use the distribution with all dependencies
java -jar dist/tn5250j-0.8.0-beta2-run/tn5250j.jar
```

## Configuration

Configuration files are stored in `~/.tn5250j` (Linux/macOS) or `%USERPROFILE%\.tn5250j` (Windows).

### Configuration Files

| File | Description |
|------|-------------|
| `sessions.properties` | Session configurations (host, device name, etc.) |
| `macros.properties` | Macro definitions |
| `keymap.properties` | Custom key mappings |
| `TN5250JDefaults.props` | Default settings |

### Custom Key Mappings

Edit `keymap.properties` in `~/.tn5250j`:

```properties
# Example: Change Enter to Right Ctrl key
Enter=10,true,false,false,false

# Key codes:
# 0=Unassigned    9=TAB        10=Enter     27=Escape
# 37=Left Arrow   38=Up Arrow   39=Right Arrow 40=Down Arrow
# 12=Clear        33=F1        34=F2        ... 48=F12
# 127=Delete      155=Insert   157=Right Ctrl
# 150=Right Shift 151=Right Alt 152=Right GUI
```

### Macro Definitions

Edit `macros.properties` in `~/.tn5250j`:

```properties
# Example: Create a macro to type "CALL MYPROGRAM"
mac.1=type(CALL MYPROGRAM\r)
```

### Custom Settings Directory

```bash
java -Duser.home=/path/to/settings -jar build/tn5250j.jar
# or
java -Demulator.settingsDirectory=/path/to/settings -jar build/tn5250j.jar
```

### Wildcard Device Names

This fork supports wildcard characters in device names:
- Use `*` or `=` as placeholder for random A-Z character
- Example: `AA999BB*` becomes `AA999BBA`, `AA999BBB`, etc. (random per connection)

## Supported Platforms

- Linux
- macOS
- Windows
- Any platform with Java 8+

## License

GPL-2.0

## Security

This fork has been reviewed for security concerns. The code is a legitimate 5250 terminal emulator for IBM i (AS/400).

### Security Findings

| Area | Status | Notes |
|------|--------|-------|
| External Commands | OK | Only for browser launch and STRPCCMD (legitimate IBM i function) |
| Network/Sockets | OK | SSL/TLS for secure IBM i connections |
| Password Handling | OK | Passwords stored in memory only, not hardcoded |
| SQL Injection | OK | JDBC uses parameterized queries |
| File Operations | OK | Only for configuration and export |
| Wildcard Feature | OK | Generates only random A-Z characters |

### External Exec Usage

The code contains legitimate uses of `Runtime.exec()`:
- **Browser launch**: Opens URLs in system default browser
- **STRPCCMD**: IBM i remote command execution (server-initiated)
- **Spool Export**: Currently commented out

This is standard Java functionality used by many applications.

This project was created because there was no terminal emulator for Linux with features like continued edit fields, gui windows, cursor progression fields, etc.

It was then open sourced to give something back to all those hackers and code churners that work so hard to provide the Linux and Open Source communities with quality work and software.

The original developer wanted it to work on different operating systems, thus Java giving the “J” at the end.

## Hosting

The project was previous hosted at [sourceforge.net](https://sourceforge.net/projects/tn5250j/). But since 2016 has been migrated to GitHub.
