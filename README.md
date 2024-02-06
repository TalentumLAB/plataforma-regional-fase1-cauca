Proyecto Aulas Steam
====================

Contenido
---------

*   [Requisitos](#requisitos)
*   [Descripción](#descripcion)
*   [Uso](#uso)
    *   [Instrucciones](#instrucciones)
*   [Docker-Compose](#docker-compose)
    *   [Servicios](#servicios)
    *   [Volúmenes](#volúmenes)
    *   [Redes](#redes)

* * *

Requisitos
----------

*   Docker version 19.03.8 o superior
*   Docker Compose version v2.20 o superior
*   git version 2.20.1 o superior
*   zip version 3.0 o superir
*   wget version 1.20.1 o superior
*   Carpetas de moodle y moodledata ubicadas en la carpeta moodle del repositorio
*   Archivos de base de datos ubicados en la carpeta de databases

Descripción
-----------

El proyecto Aulas Steam utiliza Docker Compose para orquestar varios servicios necesarios para ejecutar la solución. Estos servicios incluyen bases de datos como PostgreSQL y MariaDB, así como aplicaciones como Keycloak, un backend y un frontend.

Uso
---

### Instrucciones

1.  Crear carpeta para clonar el proyecto y navegar hacia la carpeta
    ```
    mkdir /repositories

    cd /repositories
    ```
2.  Clonar este repositorio y navegar hacia la carpeta.
    ```
    git clone https://github.com/TalentumLAB/plataforma-regional-fase1-narino.git

    cd plataforma-regional-fase1-narino
    ```
3.  Descargar contenido del lms
    ```
    cd moodle

    wget https://por_definir/moodle.zip

    wget https://por_definir/moodledata.zip
    ```

4. Asignar permisos a carpetas de lms
    ```
    chown -R www-data: moodle
    chown -R www-data: moodledata
    chmod -R 755 moodle
    chmod -R 755 moodledata
    ```
5.  Descargar archivo .sql de la base de datos de moodle.
    ```
    cd databases/moodle

    wget https://por_definir/moodledb.sql
    ```
6.  Regresar a directorio raiz y a ejecutar el archivo docker compose:
    ```
    docker-compose up -d
    ```

    Esto iniciará todos los servicios en segundo plano.

7.  Acceder a las aplicaciones a través de los siguientes enlaces:

*   Keycloak: [http://172.19.0.214:8080](http://172.19.0.214:8080)
*   Backend: [http://172.19.0.214:4000](http://172.19.0.214:4000)
*   Frontend: [http://172.19.0.214:3000](http://172.19.0.214:3000)
*   Moodle: [http://172.19.0.214:5000](http://172.19.0.214:5000)
*   Mailhog (para pruebas de correo): [http://172.19.0.214:8025](http://172.19.0.214:8025)

8.  Probar los aplicativos

    Para probar el sistema de informacion y el LMS se puede hacer con las siguientes credeciales:

    *   Usuario: docenteprueba
    *   Contraseña: password

9.  Detener los servicios cuando se haya terminado:


```
docker-compose down
```

* * *

Docker-Compose
--------------

### Servicios

*   **keycloak\_db**: Base de datos PostgreSQL para Keycloak.
*   **mailhog**: Herramienta de prueba para correos electrónicos.
*   **mariadb**: Base de datos MariaDB para la aplicación.
*   **mariadb2**: Otra instancia de MariaDB para una segunda base de datos.
*   **keycloak**: Plataforma de gestión de identidad y acceso.
*   **backend**: Backend de la aplicación Aulas Steam Reporter.
*   **frontend**: Frontend de la aplicación Aulas Steam Reporter.
*   **moodle**: Aplicación Moodle.

### Volúmenes

*   **pgdata**: Volumen persistente para la base de datos PostgreSQL.
*   **mariadb1**: Volumen persistente para la base de datos MariaDB (primera instancia).
*   **mariadb2**: Volumen persistente para la base de datos MariaDB (segunda instancia).

### Redes

*   **aulas-steam-net**: Red de puente para la comunicación entre los servicios.
