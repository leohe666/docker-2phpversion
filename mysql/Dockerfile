ARG MYSQL_VERSION
FROM mysql:${MYSQL_VERSION}
RUN touch /tmp/slow.log \
    && usermod -u 1000 mysql \