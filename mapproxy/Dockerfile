#--------- Generic stuff all our Dockerfiles should start with so we get caching ------------
FROM python:3.4
MAINTAINER thinkWhere Ltd<info@thinkwhere.com>

# Based on the docker recipe by Tim Sutton https://github.com/kartoza/docker-mapproxy

# Use local cached debs from host (saves your bandwidth!)
# Change ip below to that of your apt-cacher-ng host
# Or comment this line out if you do not with to use caching

RUN apt-get -y update

#-------------Application Specific Stuff ----------------------------------------------------

RUN apt-get install -y \
    python-imaging \
    python-yaml \
    libproj0 \
    libgeos-dev \
    python-lxml \
    libgdal-dev \
    build-essential \
    python3-dev \
    libjpeg-dev \
    zlib1g-dev \
    libfreetype6-dev \
    python-virtualenv
RUN pip install --upgrade pip
RUN pip install Shapely Pillow MapProxy==1.9.0 uwsgi requests geojson
RUN pip install --pre schematics

ADD uwsgi.ini /uwsgi.ini
RUN chmod 0755 /uwsgi.ini
ADD start.sh /start.sh
RUN chmod 0755 /start.sh
# Temp fix for coverages until next version of MapProxy available
# COPY geom.py /usr/local/lib/python3.4/site-packages/mapproxy/util/geom.py

#USER www-data
# Now launch mappproxy in the foreground
# The script will create a simple config in /mapproxy
# if one does not exist. Typically you should mount
# /mapproxy as a volume
CMD /start.sh
