# BackendDockerDev


<!-- Setup notes: getting started

Why? Because git and mounted storage volumes don't always play well together with required container permissions

What's affected?

So far, .gitkeep files may require removal from mounted directories and the pgadmin directory needs to be owned by pgadmin USER and/or GROUP whose UID/GID is 5050

Solution:
>$ chown -R 5050:5050 ./pgsql/pgadmin


For Microsoft SQL server containers there's another permissions related error if any other image selected than 2017-latest

Solution:
use mcr.microsoft.com/mssql/server:2017-latest image


For more information concerning 



- pgadmin4 containers: https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html

- mysql containers: https://hub.docker.com/_/mysql/

- mssql containers: https://hub.docker.com/_/microsoft-mssql-server

- mssql mlservices container build: 

# https://github.com/MicrosoftDocs/sql-docs/blob/live/docs/linux/sql-server-linux-setup-machine-learning-docker.md

# git clone https://github.com/microsoft/mssql-docker mssql-docker
# cd /mssql-docker/linux/preview/examples/mssql-mlservices
# docker build -t mssql-server-mlservices .


https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices

-->