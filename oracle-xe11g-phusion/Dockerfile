# derived from wnameless/oracle-xe-11g
# credit: 99% to Wei-Ming Wu

# Changes to nameless/oracle-xe-11g:
# Based on phusion/baseimage
# Installing oracle as phusion service
# Respecting NLS_LANG env for db creation

FROM phusion/baseimage:0.11
LABEL maintainer "griezma@gmail.com"
LABEL priorwork "Wei-Ming Wu <wnameless@gmail.com>"

ADD assets /assets
ARG NLS_LANG
ENV NLS_LANG ${NLS_LANG:-GERMAN_GERMANY.AL32UTF8}

RUN /assets/setup.sh

EXPOSE 22
EXPOSE 1521
EXPOSE 8080

# Give children processes n seconds to timeout
ENV KILL_PROCESS_TIMEOUT=10
# Give all other processes (such as those which have been forked) n seconds to timeout
ENV KILL_ALL_PROCESSES_TIMEOUT=20

ENV ORACLE_DATA /u01/app/oracle/oradata
# see phusion/baseimages (https://github.com/phusion/baseimage-docker) docs...

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ONBUILD RUN /usr/sbin/startup.sh

COPY runit_oracle.sh /etc/service/oracle/run
RUN chmod +x /etc/service/oracle/run

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

