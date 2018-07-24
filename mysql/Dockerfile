FROM mysql:8.0.11

# Write Permission
RUN apt-get update && apt-get install -y procps vim
RUN usermod -u 1000 mysql && chown mysql.mysql /var/run/mysqld/

EXPOSE 3306
VOLUME ["/opt"]
