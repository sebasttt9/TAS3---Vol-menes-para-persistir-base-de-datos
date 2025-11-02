1. Título

Práctica: Uso de contenedores Docker con un servidor PostgreSQL y comprobación de persistencia de datos

2. Tiempo de duración

Aproximadamente 50 minutos, dependiendo de la velocidad del estudiante y si le funciona bien el internet.

3. Fundamentos

En esta práctica vamos a trabajar con Docker, que es como una herramienta para crear "cajitas" llamadas contenedores donde se pueden ejecutar programas sin necesidad de instalarlos directo en la computadora. Esas cajas tienen todo lo que necesitan adentro para funcionar, como su sistema, sus archivos, etc. En este caso vamos a usar PostgreSQL, que es un motor de base de datos muy usado.

El problema de los contenedores es que cuando se borran, también se borran los datos, a menos que usemos algo llamado volúmenes, que sirven como carpetas que viven fuera del contenedor y guardan la información aunque el contenedor muera. Esto es útil porque en la vida real nadie quiere perder sus datos solo porque reinició un servidor.

También vamos a usar programas como DataGrip o TablePlus, que son herramientas visuales para conectarnos a la base de datos, porque hacerlo por consola a veces es complicado.

Idea clave:

Sin volumen → los datos se pierden

Con volumen → los datos se guardan incluso si el contenedor desaparece


4. Conocimientos previos

Antes de hacer esta práctica, el estudiante debería tener una idea de:
Comandos básicos de Linux (cd, ls, docker, etc.)
Saber abrir y usar un navegador
Saber instalar y abrir un programa tipo TablePlus, DBeaver, etc.
Saber lo que es una base de datos y una tabla (muy básico)
Tener idea de qué es un contenedor, aunque sea por encima

5. Objetivos a alcanzar

Crear contenedores con PostgreSQL usando Docker
Manipular archivos y configuraciones de Docker
Comprobar qué pasa con los datos cuando se elimina un contenedor
Usar un volumen y demostrar que los datos no desaparecen
Conectar un cliente gráfico a una base de datos dentro de Docker

6. Equipo necesario

Una computadora con Windows, Linux o macOS
Internet (si no hay, no se puede bajar imágenes de Docker)
Docker instalado (cualquier versión reciente)
Cuenta en Docker Hub o Docker Play (por si se hace en web)
Client DB opcional: DBeaver, TablePlus, DataGrip, etc.

7. Material de apoyo

Documentación oficial de Docker
Guía de la asignatura
Cheat sheet de comandos básicos de Linux
Documentación de PostgreSQL (si hace falta buscar comandos)

8. Procedimiento
Parte 1: Base de datos sin volumen

Paso 1: Crear el contenedor PostgreSQL

docker run --name server_db1 -e POSTGRES_PASSWORD=admin -d postgres


Paso 2: Abrir DataGrip/TablePlus y conectarse

Host: localhost

Puerto: 5432

Usuario: postgres

Password: admin

Paso 3: Crear BD test, tabla customer e insertar 1 registro

Paso 4: Borrar el contenedor

docker stop server_db1
docker rm server_db1


Paso 5: Volver a crearlo igual que antes y conectarse otra vez
Resultado: la base de datos y la tabla ya NO existen.

Parte 2: Base de datos con volumen

Paso 1: Crear volumen

docker volume create pgdata

Paso 2: Crear contenedor con volumen

docker run --name server_db2 -e POSTGRES_PASSWORD=admin -v pgdata:/var/lib/postgresql/data -d postgres

Paso 3: Conectar, crear BD, tabla y registro igual que antes

Paso 4: Eliminar el contenedor

docker stop server_db2
docker rm server_db2


Paso 5: Volver a crearlo usando el mismo volumen

docker run --name server_db2 -e POSTGRES_PASSWORD=admin -v pgdata:/var/lib/postgresql/data -d postgres

10. Bibliografía

Docker, Inc. (2025). PostgreSQL image. Docker Hub. Recuperado de https://hub.docker.com/_/postgres

PostgreSQL Global Development Group. (2025). PostgreSQL Documentation. Recuperado de https://www.postgresql.org/docs/

Merkel, D. (2014). Docker: Lightweight Linux containers for consistent development and deployment. Linux Journal.
