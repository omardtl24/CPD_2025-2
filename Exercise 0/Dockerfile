# Imagen base con JDK 8 + Maven
FROM maven:3.9.9-eclipse-temurin-8

# Directorio de trabajo dentro del contenedor
WORKDIR /app

# Instalar la librería PCDP en el repo local de Maven
RUN git clone https://github.com/habanero-rice/pcdp.git /tmp/pcdp && \
    cd /tmp/pcdp && \
    mvn clean install -DskipTests && \
    rm -rf /tmp/pcdp

# Copiar archivos de proyecto (solo Exercise 0)
COPY . /app

# Compilar proyecto (se salta tests aquí para no fallar build)
RUN mvn clean package -DskipTests