## Reproducer for issue #24, see [https://github.com/cescoffier/quarkus-todo-app/issues/24]

This repo is basically the same as https://github.com/cescoffier/quarkus-todo-app but with the following 2 files added:
1. Dockerfile in repo-dir/quarkus-todo
2. docker-compose.yml in repo-dir/quarkus-todo

Environment:
* Maven home: C:\Program Files\Maven\apache-maven-3.6.3
* Java version: 11.0.8, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk-11.0.8
* Default locale: de_DE, platform encoding: Cp1252
* OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"

Steps to reproduce the issue:
1. clone this repo
2. cd repo-dir/quarkus-todo
3. mvn clean
4. Launch docker
5. docker-compose up

Upon this, I'm getting the following exception mesagges in the console (exerpt):
`
db_1                    | PostgreSQL init process complete; ready for start up.
db_1                    |
db_1                    | 2021-04-26 07:53:22.004 UTC [1] LOG:  starting PostgreSQL 13.2 (Debian 13.2-1.pgdg100+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 8.3.0-6) 8.3.0, 64-bit
db_1                    | 2021-04-26 07:53:22.004 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
db_1                    | 2021-04-26 07:53:22.004 UTC [1] LOG:  listening on IPv6 address "::", port 5432
db_1                    | 2021-04-26 07:53:22.010 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
db_1                    | 2021-04-26 07:53:22.017 UTC [75] LOG:  database system was shut down at 2021-04-26 07:53:21 UTC
db_1                    | 2021-04-26 07:53:22.023 UTC [1] LOG:  database system is ready to accept connections
quarkus-todo-backend_1  | __  ____  __  _____   ___  __ ____  ______
quarkus-todo-backend_1  |  --/ __ \/ / / / _ | / _ \/ //_/ / / / __/
quarkus-todo-backend_1  |  -/ /_/ / /_/ / __ |/ , _/ ,< / /_/ /\ \
quarkus-todo-backend_1  | --\___\_\____/_/ |_/_/|_/_/|_|\____/___/
quarkus-todo-backend_1  | 2021-04-26 07:53:24,769 INFO  [io.agr.pool] (main) Datasource '<default>': Initial size smaller than min. Connections will be created when necessary
quarkus-todo-backend_1  | 2021-04-26 07:53:24,967 WARN  [io.agr.pool] (agroal-11) Datasource '<default>': Connection to localhost:5432 refused. Check that the hostname and port are correct an
d that the postmaster is accepting TCP/IP connections.
quarkus-todo-backend_1  | 2021-04-26 07:53:24,968 WARN  [org.hib.eng.jdb.env.int.JdbcEnvironmentInitiator] (main) HHH000342: Could not obtain connection to query metadata: org.postgresql.util
.PSQLException: Connection to localhost:5432 refused. Check that the hostname and port are correct and that the postmaster is accepting TCP/IP connections.
quarkus-todo-backend_1  |       at org.postgresql.core.v3.ConnectionFactoryImpl.openConnectionImpl(ConnectionFactoryImpl.java:303)
quarkus-todo-backend_1  |       at org.postgresql.core.ConnectionFactory.openConnection(ConnectionFactory.java:51)
quarkus-todo-backend_1  |       at org.postgresql.jdbc.PgConnection.<init>(PgConnection.java:225)
quarkus-todo-backend_1  |       at org.postgresql.Driver.makeConnection(Driver.java:465)
quarkus-todo-backend_1  |       at org.postgresql.Driver.connect(Driver.java:264)
quarkus-todo-backend_1  |       at io.agroal.pool.ConnectionFactory.createConnection(ConnectionFactory.java:200)
quarkus-todo-backend_1  |       at io.agroal.pool.ConnectionPool$CreateConnectionTask.call(ConnectionPool.java:452)
quarkus-todo-backend_1  |       at io.agroal.pool.ConnectionPool$CreateConnectionTask.call(ConnectionPool.java:434)
quarkus-todo-backend_1  |       at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
`