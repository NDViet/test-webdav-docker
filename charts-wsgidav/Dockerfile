FROM python:alpine

#======================================
# Add dependencies
#======================================
RUN apk add --no-cache --update supervisor bash \
    && pip install --upgrade wsgidav \
    && pip install --upgrade cheroot lxml \
    && rm -rf /tmp/* /var/cache/apk/*

RUN mkdir -p /webdav/share /srv/data/share

COPY src/main/resources/config.yaml /webdav/

WORKDIR /webdav/

#======================================
# Add Supervisor configuration files
#======================================
RUN  mkdir -p /var/run/supervisor /var/log/supervisor \
    && cd /opt/bin \
    && pip install psutil

COPY src/main/resources/entry_point.sh /opt/bin/
COPY src/main/resources/supervisord.conf /etc/
COPY src/main/resources/webdav.sh /opt/bin/

ENTRYPOINT ["/opt/bin/entry_point.sh"]
CMD ["/opt/bin/entry_point.sh"]

#ENV

EXPOSE 8080