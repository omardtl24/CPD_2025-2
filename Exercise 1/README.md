# Exercise 1

This document explains how to run the Exercise 1 project both with Docker and locally using Maven.

## Run locally (Maven)

Prerequisite: JDK and Maven installed.

1. Compile the project:

```bash
mvn -f "Exercise 1/pom.xml" compile
```

2. Run the tests:

```bash
mvn -f "Exercise 1/pom.xml" test
```

Notes:
- The `Exercise 1` folder contains additional jars (`hamcrest-core-1.3.jar`, `junit-4.12.jar`, `pcdp-core-0.0.4-SNAPSHOT.jar`) which some environments may reference. Using Maven will usually fetch or use the configured dependencies from the `pom.xml`.
- If you run from the repository root, the `-f` flag points Maven to the correct pom.

## Run with Docker

Prerequisite: Docker installed and running.

From the repository root run the following commands to build and run the image.

1. Build the Docker image (tag it `exercise1`):

```bash
docker build -t exercise1 "Exercise 1"
```

2. Run the container (the Dockerfile may run tests at build or on container start depending on its contents):

```bash
docker run --rm exercise1
```

Notes:
- The image build may run `mvn` inside the container. If the `Dockerfile` is configured to run tests during image build, you will see test output during `docker build`.
- To run Maven commands interactively inside a Maven image while mounting the project sources:

```bash
docker run --rm -it -v "$PWD/Exercise 1":/workspace -w /workspace maven:3.8.8-openjdk-17 bash
# then inside the container:
mvn compile
mvn test
```
