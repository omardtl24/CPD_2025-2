# Exercise 0

This document explains how to run the Exercise 0 project both with Docker and locally using Maven.

## Run locally (Maven)

Prerequisite: JDK and Maven installed.

1. Compile the project:

```bash
mvn -f "Exercise 0/pom.xml" compile
```

2. Run the tests:

```bash
mvn -f "Exercise 0/pom.xml" test
```

Notes:
- The project already includes a `Dockerfile` in the `Exercise 0` folder.
- If you need to run from the repository root, the `-f` flag points Maven to the correct pom.

## Run with Docker

Prerequisite: Docker installed and running.

From the repository root run the following commands to build and run the image.

1. Build the Docker image (tag it `exercise0`):

```bash
docker build -t exercise0 "Exercise 0"
```

2. Run the container (the Dockerfile may run tests at build or on container start depending on its contents):

```bash
docker run --rm exercise0
```

Notes:
- The image build may run `mvn` inside the container. If the `Dockerfile` is configured to run tests during image build, you will see test output during `docker build`.
- If you want to run Maven commands interactively inside a container, you can start a shell in the image and run them there:

```bash
docker run --rm -it -v "$PWD/Exercise 0":/workspace -w /workspace maven:3.8.8-openjdk-17 bash
# then inside the container:
mvn compile
mvn test
```
