FROM php:8.2-fpm

# Install freetds and odbc drivers
RUN apt-get update \
&& apt-get install -y unixodbc \
&& apt-get install -y unixodbc-dev \
&& apt-get install -y tdsodbc \
&& apt-get install -y freetds-bin \
&& apt-get install -y freetds-common \
&& apt-get install -y freetds-dev \
&& apt-get install -y vim \
&& apt-get install -y iputils-ping \
&& apt-get install -y net-tools \
&& apt-get install -y libpq-dev

# Copy freetds and odbc files for mssql connection
COPY freetds.conf /etc/freetds/
COPY odbc.ini /etc/
COPY odbcinst.ini /etc/

RUN docker-php-ext-install pdo \
&& docker-php-ext-install pdo_mysql \
&& docker-php-ext-install pgsql pdo_pgsql \
&& docker-php-ext-configure pdo_odbc --with-pdo-odbc=unixODBC,/usr \
&& docker-php-ext-install pdo_odbc pdo_dblib

#  zip
# pdo_dblib => NEEDS FREETDS
# pgsql pdo_pgsql odbc pdo_odbc pdo_sqlite oci8 pdo_oci
