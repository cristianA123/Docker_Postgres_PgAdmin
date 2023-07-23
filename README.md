# Docker Compose con Volumen y sin Volumen (Bind Volumes)

### Docker compose con Volumen:

- Unir Base de datos con cliente en un solo volumen

  - PostgreSQL
  - PGAdmin

  ```

    version: 3
    services:
    db:
    container_name: postgres_database
    image: postgres:15.1
    volumes: - postgres-db:/var/lib/postgresql/data
    environment: - POSTGRES_PASSWORD=123456

    pgAdmin:
    depends_on: - db
    image: dpage/pgadmin4:6.17
    ports: - "8080:80"
    environment: - PGADMIN_DEFAULT_PASSWORD=123456 - PGADMIN_DEFAULT_EMAIL=superman@google.com

    volumes:
    postgres-db:
    external: true

    ```

### Docker compose sin Volumen:

- Unir Base de datos con cliente en un solo volumen
  - PostgreSQL (local)
  - PGAdmin (local)


  ```
    version: 3

    services:
    db:
        container_name: postgres_database
        image: postgres:15.1
        volumes:
        # - postgres-db:/var/lib/postgresql/data # ejemplo
        - ./postgres:/var/lib/postgresql/data
        environment:
        - POSTGRES_PASSWORD=123456

    pgAdmin:
        depends_on:
        - db
        image: dpage/pgadmin4:6.17
        ports:
        - "8080:80"
        volumes:
        - ./pgadmin:/var/lib/pgadmin
        environment:
        - PGADMIN_DEFAULT_PASSWORD=123456 
        - PGADMIN_DEFAULT_EMAIL=superman@google.com

  ```
