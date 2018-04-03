# app-uwsgi

FROM debian:jessie
ENV REFRESHED 20171128
RUN apt-get update \
        && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
		build-essential \
		libpcre3 \
		libpcre3-dev \
		python-dev \
                python-pip \
                python-psycopg2 \
        && rm -fr /var/lib/apt/lists/* \
        && rm -fr /tmp/* \
        && rm -fr /var/tmp/*

# Set up package and requirements
RUN pip install "django<2" uwsgi whitenoise
RUN	mkdir /data
WORKDIR /data
COPY requirements.txt /data
RUN pip install -r /data/requirements.txt
COPY uwsgi.ini /etc/uwsgi.ini

ENTRYPOINT ["/usr/local/bin/uwsgi", "/etc/uwsgi.ini"]
