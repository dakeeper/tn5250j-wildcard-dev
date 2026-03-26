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

## Supported Platforms

- Linux
- macOS
- Windows
- Any platform with Java 8+

## License

GPL-2.0

This project was created because there was no terminal emulator for Linux with features like continued edit fields, gui windows, cursor progression fields, etc.

It was then open sourced to give something back to all those hackers and code churners that work so hard to provide the Linux and Open Source communities with quality work and software.

The original developer wanted it to work on different operating systems, thus Java giving the “J” at the end.

## Hosting

The project was previous hosted at [sourceforge.net](https://sourceforge.net/projects/tn5250j/). But since 2016 has been migrated to GitHub.
