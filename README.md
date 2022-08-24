# BackendDockerDev


<!-- Setup notes: getting started

Why? Because git and mounted storage volumes don't always play well together with required container permissions

What's affected? So far, .gitkeep files may require removal and the pgadmin admin directory needs to be owned by pgadmin USER and/or GROUP whose UID/GID is 5050

Correction:
>$ chown -R 5050:5050 ./pgsql/pgadmin

For more information concerning 



- pgadmin4 containers: https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html

- mysql containers: https://hub.docker.com/_/mysql/

- mssql containers:


-->