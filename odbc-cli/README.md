# odbc-cli

You can use a docker image to run [odbc-cli](https://detule.github.io/odbc-cli).  This image uses `unixODBC` for a driver-manager, and comes with the following drivers pre-installed (listed here by name):

* SQLite
* SQLite3
* PostgreSQL ANSI
* PostgreSQL Unicode
* MySQL ODBC 8.0 Unicode Driver
* MySQL ODBC 8.0 ANSI Driver
* ODBC Driver 17 for SQL Server

You may need to extend this docker image if you wish to make additional drivers available.  You should also note that this docker image tracks the "master" branch in the *odbc-cli* repository; as such, it should be considered the latest/development version of the client, and may be at times ahead of the version released to PyPI.

# Usage

To create a running instance of the client, use the `docker run` command.  However since `odbc-cli` requires a pre-populated INI configuration file of data-sources, you will also need to bind your config to a location where unixODBC (the driver manager in the image) can locate it.

```
docker run --rm -it -v /location/to/your/datasources/ini/file:/root/.odbc.ini dbcliorg/odbc-cli
```

Recall, your data-sources INI file may look like:

```
[mysql_db]
Description = MySQL DB
Driver = MySQL ODBC 8.0 ANSI Driver
Server = my-mysql2
```

For more help on formatting and content of the DSN INI file, visit the [unixODBC documentation](http://www.unixodbc.com/odbcinst.html).

If you want to use a specific client config

```
docker run --rm -it -v /location/to/your/config/directory:/root/.config/odbcli -v /location/to/your/datasources/ini/file:/root/.odbc.ini dbcliorg/odbc-cli
```

To save yourself typing this expression out whenever you want to run the client, you can use alias

On linux

```
alias odbc-cli="docker run --rm -it -v /location/to/your/datasources/ini/file:/root/.odbc.ini dbcliorg/odbc-cli"
odbc-cli
```

On Windows

```
@doskey odbc-cli=docker run --rm -it -v /location/to/your/datasources/ini/file:/root/.odbc.ini dbcliorg/odbc-cli
odbc-cli
```
