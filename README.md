# TN5250J

A 5250 terminal emulator for the IBM i (AS/400) written in Java.

This fork adds wildcard support for device names:
- Use `*` or `=` in device name as placeholder for random A-Z character
- Example: `AA999BB*` becomes `AA999BBA`, `AA999BBB`, etc. (random)

Documentation is available at: [tn5250j.github.io](https://tn5250j.github.io/)

[![Build Status](https://travis-ci.org/tn5250j/tn5250j.svg?branch=travis)](https://travis-ci.org/tn5250j/tn5250j)

## Build from Source

### Prerequisites

- Java JDK 8 or higher
- Apache Ant

### Build Steps

```bash
# Clone the repository
git clone https://github.com/dakeeper/tn5250j-wildcard-dev.git
cd tn5250j-wildcard-dev

# Build the project
ant compile package

# Create distribution with dependencies
ant dist-run-prepare
```

### Running

After building, run the application:

```bash
# Using the compiled JAR
java -jar build/tn5250j.jar

# Or use the distribution with all dependencies
java -jar dist/tn5250j-0.8.0-beta2-run/tn5250j.jar
```

## History

This project was created because there was no terminal emulator for Linux with features like continued edit fields, gui windows, cursor progression fields, etc.

It was then open sourced to give something back to all those hackers and code churners that work so hard to provide the Linux and Open Source communities with quality work and software.

The original developer wanted it to work on different operating systems, thus Java giving the “J” at the end.

## Hosting

The project was previous hosted at [sourceforge.net](https://sourceforge.net/projects/tn5250j/). But since 2016 has been migrated to GitHub.
