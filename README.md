MySQL + Hibernate + Redis Cache Tutorial (Proyecto Final JRU Módulo 4)

Este proyecto es un tutorial práctico que muestra cómo optimizar consultas frecuentes en una base de datos MySQL utilizando Redis como sistema de almacenamiento en memoria tipo key-value.

El objetivo es comparar el rendimiento entre consultar datos directamente en MySQL y obtenerlos desde Redis, donde se almacenan únicamente los campos más solicitados.

🚀 Tecnologías utilizadas

Java 17

Hibernate (ORM)

MySQL

Redis

Docker / Docker Compose

IDEA Ultimate

redis-insight (opcional)

🗂️ Arquitectura del proyecto

El proyecto sigue una estructura simple basada en capas:

domain/ – Entidades (Country, City, CountryLanguage)

dao/ – Acceso a datos con Hibernate

service/ – Lógica de negocio y cacheo en Redis

util/ – Configuración de Hibernate y Redis

📌 Objetivo del proyecto

En la base de datos existe una relación:

Country → City
Country → Language


Las ciudades son consultadas con mucha frecuencia, lo cual puede volver lento el sistema si siempre se consulta MySQL.

Por ello:

Obtenemos datos desde MySQL usando Hibernate.

Transformamos los datos a un formato ligero (JSON).

Guardamos solo esos datos en Redis.

Cuando el usuario solicita un dato ya cacheado, se devuelve desde Redis.

Comparamos el rendimiento entre MySQL y Redis.

🛠️ Plan de trabajo del proyecto

Iniciar Docker.

Ejecutar contenedores de MySQL y Redis.

Importar el dump SQL.

Crear el proyecto Maven en IntelliJ.

Configurar dependencias (Hibernate, Redis/Jedis o Lettuce).

Crear entidades Hibernate.

Crear DAOs para leer información desde MySQL.

Crear método que transforma los datos a JSON.

Escribir los datos más consultados en Redis.

Leer datos desde Redis.

Comparar los tiempos de acceso.

⏱️ Comparación de rendimiento

El proyecto incluye pruebas de velocidad aproximadas:

Consulta MySQL: más lenta

Consulta Redis: extremadamente rápida (milisegundos)

Esto demuestra el beneficio de usar Redis como caché en sistemas donde las lecturas son frecuentes.

📦 Ejecución con Docker

Ejemplo de docker-compose:

services:
  mysql:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: world
    ports:
      - "3306:3306"

  redis:
    image: redis
    ports:
      - "6379:6379"
