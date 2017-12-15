# Base python 2.7 build
# Python 2.7 | Django

FROM python:2.7


##############################################################################
# Environment variables
##############################################################################
# Get noninteractive frontend for Debian to avoid some problems:
#    debconf: unable to initialize frontend: Dialog
ENV DEBIAN_FRONTEND noninteractive

##############################################################################
# OS Updates and Python packages
##############################################################################

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y

RUN apt-get install -y apt-utils
# Libs required for geospatial libraries on Debian...
RUN apt-get -y install binutils libproj-dev gdal-bin

##############################################################################
# A Few pip installs not commonly in requirements.txt
##############################################################################

RUN apt-get install -y nano wget
# build dependencies for postgres and image bindings
RUN apt-get install -y python-imaging python-psycopg2

##############################################################################
# setup startup script for gunicord WSGI service
##############################################################################

#RUN groupadd webapps
#RUN useradd webapp -G webapps
#RUN mkdir -p /var/log/webapp/ && chown -R webapp /var/log/webapp/ && chmod -R u+rX /var/log/webapp/
#RUN mkdir -p /var/run/webapp/ && chown -R webapp /var/run/webapp/ && chmod -R u+rX /var/run/webapp/

##############################################################################
# Install and configure supervisord
##############################################################################

#RUN apt-get install -y supervisor
#RUN mkdir -p /var/log/supervisor
#ADD ./deploy/supervisor_conf.d/webapp.conf /etc/supervisor/conf.d/webapp.conf

##############################################################################
# Install dependencies and run scripts.
##############################################################################

RUN mkdir -p /var/projects/project1
COPY requirements.txt /var/projects/project1/
RUN pip install -r /var/projects/project1/requirements.txt
COPY . /var/projects/project1
WORKDIR /var/projects/project1

##############################################################################
# Run start.sh script when the container starts.
# Note: If you run migrations etc outside CMD, envs won't be available!
##############################################################################
CMD ["sh", "./deploy/container_start.sh"]

# Expose listen ports
EXPOSE 8002
