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
nano docker-compose.yml
```

**Creamos nuestro docker-compose:**
```bash

services: #array de los servicios que vamos a utilizar
  web:
    image: odoo:17.0 #version 17 de odoo
    container_name: odooWebContainer #nombre del contenedor
    restart: unless-stopped #hacemos que el servicio continúe hasta que lo detengamos manualmente
    depends_on:
      - db
    ports: #indicamos el puerto de acceso
      - "8069:8069"
    environment:
      - HOST=db
      - USER=adrian
      - PASSWORD=adrian
    volumes: #realizamos la persistencia de datos para prevenir perdida de datos en caso de fallo.
      - odoo-web-data:/var/lib/odoo



  db:
    image: postgres:15 #imagen postgress 15, la recomendada en dockerhub
    container_name: postgresSQLContainer #nombre del contenedor
    restart: unless-stopped #hacemos que el servicio continúe hasta que lo detengamos manualmente
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=adrian
      - POSTGRES_USER=adrian
    volumes: #realizamos la persistencia de datos para prevenir perdida de datos en caso de fallo.
      - odoo-db-data:/var/lib/postgresql/data
    ports: #puerto por defecto para postgresSQL
      - "5432:5432"

  pgadmin:
    restart: unless-stopped #hacemos que el servicio continúe hasta que lo detengamos manualmente
    image: dpage/pgadmin4:latest #La versión más reciente de PgAdmin
    container_name: PgAdminContainer
    depends_on: #indicamos que PgAdmin depende de la base de datos para iniciar para que PgAdmin no inicie antes
      - db
    ports: #puerto de acceso
      - "5050:80"
    environment:
      - PGADMIN_DEFAULT_EMAIL= aabeijoncarbajo@danielcastelao.org
      - PGADMIN_DEFAULT_PASSWORD= adrian123
    volumes: #realizamos la persistencia de datos para prevenir perdida de datos en caso de fallo.
      - pgadmin-data:/var/lib/pgadmin


volumes: # volumenes para la persistencia de datos
  odoo-web-data:
  odoo-db-data:
  pgadmin-data:
```

```bash
docker-compose up
```
**Comprobamos que odoo nos carga correctamente, y añadimos nuestras credenciales:**

![odoo2](https://github.com/user-attachments/assets/0fe67a1e-5861-49db-95c0-6438eb692044)

**Tras una espera podemos logearnos en nuestro odoo:**

![odoo3](https://github.com/user-attachments/assets/a7013301-aaf5-4064-a3b6-ef2f052a7271)

**Comprobamos todas las herramientas que nos ofrece:**

![odoo4](https://github.com/user-attachments/assets/fdd9f8d4-4b14-4d55-b9cf-96984ddd1b58)

**Verificamos que estamos con la comunity edition:**

![odoo5](https://github.com/user-attachments/assets/8d20d666-8235-4741-a4be-e8a3fbd93e00)


### 2) Instala PgAdmin y conectala a lo BBDD.

Ya tenemos pgadmin asi que hacemos login pdadmin:

![odoo6](https://github.com/user-attachments/assets/18e2cfa2-8cc7-49b2-bece-88f0bf921fb9)

**Accedemos sin problema a pgadmin:**

![odoo7](https://github.com/user-attachments/assets/8e3cfcff-cf74-451c-b3f5-bf6682a8dfc1)

**PGAdmin no ha detectado nuestra base de datos así que tendremos que añadirla a la lista:**

![odoo8](https://github.com/user-attachments/assets/c4b9f1e4-b50f-49cd-a022-926ef8826f9c)

**Comprobamos que nuestra base de datos está funcionando en pgadmin:**

![odoo9](https://github.com/user-attachments/assets/4aa531ee-429c-4b7b-87ea-dc43e7e184a8)

### 3) Preguntas teóricas:

### ¿Que ocurre si en el ordenador local el puerto 5432 está ocupado?
Si ya tenemos ocupado el puerto nos dará error y no podremos levantar el servicio.

### ¿Y si lo estuviese el 8069?
También nos dará error, ya que el puerto está en uso no nos deja levantar el servicio.

### ¿Como puedes solucionarlo?
Podríamos matar los servicios que esten utilizando los puertos que queremos, o si no, cambiar los puertos de odoo y de postgres por otros que nos seán válidos.


---------------------------------------------

**Bibliografía enlaces:**

https://hub.docker.com/_/odoo

https://www.digitalocean.com/community/tutorials/how-to-install-odoo-with-docker-on-ubuntu
