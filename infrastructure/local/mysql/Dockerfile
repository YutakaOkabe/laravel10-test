FROM mysql:8.0-debian

ARG MYSQL_USER_ID=${MYSQL_USER_ID}

RUN usermod -u ${MYSQL_USER_ID} mysql

RUN apt-get update && apt-get install -y locales \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/run/mysqld && \
  chmod -R 777 /var/run/mysqld
