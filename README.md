# baq

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: <https://quarkus.io/>.

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:

```shell script
./mvnw quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at <http://localhost:8080/q/dev/>.

## Packaging and running the application

The application can be packaged using:

```shell script
./mvnw package
```

It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:

```shell script
./mvnw package -Dquarkus.package.jar.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using:

```shell script
./mvnw package -Dnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using:

```shell script
./mvnw package -Dnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/baq-1.0.0-runner`

If you want to learn more about building native executables, please consult <https://quarkus.io/guides/maven-tooling>.

## Related Guides

- REST ([guide](https://quarkus.io/guides/rest)): A Jakarta REST implementation utilizing build time processing and Vert.x. This extension is not compatible with the quarkus-resteasy extension, or any of the extensions that depend on it.
- Hibernate ORM ([guide](https://quarkus.io/guides/hibernate-orm)): Define your persistent model with Hibernate ORM and Jakarta Persistence
- JDBC Driver - MariaDB ([guide](https://quarkus.io/guides/datasource)): Connect to the MariaDB database via JDBC
- Hibernate ORM with Panache ([guide](https://quarkus.io/guides/hibernate-orm-panache)): Simplify your persistence code for Hibernate ORM via the active record or the repository pattern

## Provided Code

### Hibernate ORM

Create your first JPA entity

[Related guide section...](https://quarkus.io/guides/hibernate-orm)

[Related Hibernate with Panache section...](https://quarkus.io/guides/hibernate-orm-panache)


### REST

Easily start your REST Web Services

[Related guide section...](https://quarkus.io/guides/getting-started-reactive#reactive-jax-rs-resources)

## Uruchomienie bazy danych (MariaDB) w Dockerze

Projekt korzysta z kierowcy MariaDB (`quarkus-jdbc-mariadb`). Aby uruchomić bazę w kontenerze:

1. Zainstaluj i uruchom Docker.
2. W terminalu wykonaj:

```bash
docker run --name baq-db \
  -e MARIADB_ROOT_PASSWORD=rootpass \
  -e MARIADB_DATABASE=baq \
  -e MARIADB_USER=baq \
  -e MARIADB_PASSWORD=baq \
  -p 3306:3306 \
  -d mariadb:latest
```

3. (Opcjonalnie) W pliku `src/main/resources/application.properties` ustaw parametry połączenia:

```
quarkus.datasource.db-kind=mariadb
quarkus.datasource.username=baq
quarkus.datasource.password=baq
quarkus.datasource.jdbc.url=jdbc:mariadb://localhost:3306/baq
quarkus.hibernate-orm.database.generation=update
```

## Uruchomienie backendu (Quarkus)

1. **Tryb developerski** – umożliwia live coding:

```bash
./mvnw quarkus:dev
```

(uruchamia serwer na `http://localhost:8080`)

2. **Tryb produkcyjny** – zbuduj aplikację i uruchom JAR:

```bash
./mvnw package
java -jar target/quarkus-app/quarkus-run.jar
```

## Uruchomienie frontendu (przykład projektu Node.js)

1. Przejdź do katalogu frontendu:

```bash
cd frontend
```

2. Zainstaluj zależności i uruchom serwer deweloperski:

```bash
npm install
npm start        # albo: npm run dev
```

3. Frontend zwykle nasłuchuje na `http://localhost:3000` (lub innym porcie zgodnie z konfiguracją).  
   Upewnij się, że adresy API wskazują na działający backend (`http://localhost:8080`).

