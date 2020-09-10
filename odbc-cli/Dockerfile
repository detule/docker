FROM python:3.8-buster
ENV LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu/odbc

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
  && curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list \
  && echo "deb http://apt.postgresql.org/pub/repos/apt buster-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
  && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && wget --quiet -O /tmp/mysql-connector-odbc_8.0.21-1debian10_amd64.deb https://dev.mysql.com/get/Downloads/Connector-ODBC/8.0/mysql-connector-odbc_8.0.21-1debian10_amd64.deb \
  && apt-get update

RUN ACCEPT_EULA=Y apt-get install -y \
  unixodbc-dev \
  msodbcsql17 \
  odbc-postgresql \
  libsqliteodbc \
  less

RUN apt install /tmp/mysql-connector-odbc_8.0.21-1debian10_amd64.deb
RUN odbcinst -i -d -f /opt/microsoft/msodbcsql17/etc/odbcinst.ini

RUN pip install odbcli==0.0.4
# Now install latest/development versions of cyanodbc and odbcli
RUN pip install --force-reinstall --no-deps --index-url https://test.pypi.org/simple/ cyanodbc odbcli
RUN touch /root/.odbc.ini
ENTRYPOINT ["odbc-cli"]
