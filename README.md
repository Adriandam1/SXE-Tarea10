# SXE-Tarea10

- Instala Odoo 17 Community con docker-compose.

- Instala PgAdmin y conectala a lo BBDD

Entrega el repositorio con los ficheros y en el Readme la explicación.

En el readme tiene que estar explicado las diferentes partes del docker-composer, así como los comandos para lanzar los contenedores y capturas de pantalla que demuestren la instalación de Odoo, configuración y acceso al mismo así como de PgAdmin. Es necesario incluir una captura DENTRO de Odoo para demostrar que se ha instalado y configurado correctamente y también dentro de PgAdmin (instalad primero odoo y cread una base de datos).

¿Que ocurre si en el ordenador local el puerto 5432 está ocupado? ¿Y si lo estuviese el 8069? ¿Como puedes solucionarlo?

Se valora formato del Readme, capturas, commits, funcionalidad, capturas.

----------------------------------------------------------------------------

### 1) Instala Odoo 17 Community con docker-compose.
```bash

version: '3.1'
services:
  web:
    image: odoo:17.0
    depends_on:
      - mydb
    ports:
      - "8069:8069"
    environment:
    - HOST=mydb
    - USER=odoo
    - PASSWORD=myodoo
  mydb:
    image: postgres:15
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=myodoo
      - POSTGRES_USER=odoo

```

### 3

### 4

### 5

enlaces:

https://hub.docker.com/_/odoo

https://www.digitalocean.com/community/tutorials/how-to-install-odoo-with-docker-on-ubuntu
