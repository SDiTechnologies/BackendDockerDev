# BackendDockerDev

This project seeks to be a compendium of docker container recipes for commonly used databases and other storage.

__WARNING__:

Included containers may be modified to use docker-volumes to avoid some issues encountered and documented below.

Mountable storage, though introducing permissions issues, was chosen to provide a central location within the repository to avoid addressing 'docker' system volume location variations. 

## Requirements

In order to make use of this repository, your machine requires the following software and permissions:

- [docker engine](https://docs.docker.com/engine/install/)
- [docker-compose](https://docs.docker.com/compose/install/)
- sudo and/or 'docker' group privileges

## Troubleshooting

### __Postgres Container__

Description: Starting container results in the following error.

<pre><font color="#AA00AA">postgresql |</font> The files belonging to this database system will be owned by user &quot;postgres&quot;.
<font color="#AA00AA">postgresql |</font> This user must also own the server process.
<font color="#AA00AA">postgresql |</font> 
<font color="#AA00AA">postgresql |</font> The database cluster will be initialized with locale &quot;en_US.utf8&quot;.
<font color="#AA00AA">postgresql |</font> The default database encoding has accordingly been set to &quot;UTF8&quot;.
<font color="#AA00AA">postgresql |</font> The default text search configuration will be set to &quot;english&quot;.
<font color="#AA00AA">postgresql |</font> 
<font color="#AA00AA">postgresql |</font> Data page checksums are disabled.
<font color="#AA00AA">postgresql |</font> 
<font color="#AA00AA">postgresql |</font> initdb: error: directory &quot;/var/lib/postgresql/data&quot; exists but is not empty
<font color="#AA00AA">postgresql |</font> It contains a dot-prefixed/invisible file, perhaps due to it being a mount point.
<font color="#AA00AA">postgresql |</font> Using a mount point directly as the data directory is not recommended.
<font color="#AA00AA">postgresql |</font> Create a subdirectory under the mount point.
<font color="#00AA00">postgresql exited with code 1</font>
</pre>


Source: `.gitkeep` file located inside data/pgsql/data creates errors when mounting.


Solution: Remove `.gitkeep` file.
```bash
>$ rm data/pgsql/data/.gitkeep
```

### __Postgres Admin 4 Container__

Description: Starting container results in the following error.

<pre><font color="#00AAAA">pgweb    |</font> ERROR  : Failed to create the directory /var/lib/pgadmin/sessions:
<font color="#00AAAA">pgweb    |</font>            [Errno 13] Permission denied: &apos;/var/lib/pgadmin/sessions&apos;
<font color="#00AAAA">pgweb    |</font> HINT   : Create the directory /var/lib/pgadmin/sessions, ensure it is writeable by
<font color="#00AAAA">pgweb    |</font>          &apos;pgadmin&apos;, and try again, or, create a config_local.py file
<font color="#00AAAA">pgweb    |</font>          and override the SESSION_DB_PATH setting per
<font color="#00AAAA">pgweb    |</font>          https://www.pgadmin.org/docs/pgadmin4/6.12/config_py.html
</pre>

Source: data/pgsql/pgadmin directory has incorrect permissions

Solution:
```bash
# remove the .gitkeep file
>$ rm data/pgsql/pgadmin/.gitkeep
# alter permissions of the mounted directory
# directory MUST belong to 'pgadmin' user and/or GID/UID 5050
>$ chmod -R 5050:5050 data/pgsql/pgadmin
```


<!-- Setup notes: getting started


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