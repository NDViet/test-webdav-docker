FROM python:alpine

#======================================
# Add ENV
#======================================
ENV PIP_ROOT_USER_ACTION=ignore
ENV CONFIG_FILE /opt/bin/config.yaml
ENV ROOT_PATH /share
ENV SERVER cheroot
ENV SERVER_PORT 8080

#======================================
# Add dependencies
#======================================
RUN apk add --no-cache --virtual .build-deps gcc libxslt-dev musl-dev py3-lxml py3-pip \
    && apk add --no-cache --virtual .build-deps supervisor bash \
    && python -m pip install --upgrade --no-cache-dir pip \
    && pip install --upgrade --no-cache-dir lxml \
    && pip install --upgrade --no-cache-dir ${SERVER} \
    && pip install --upgrade --no-cache-dir WsgiDAV==4.3.0 \
    && rm -rf /tmp/* /var/cache/apk/*

#======================================
# Add Supervisor configuration files
#======================================
RUN  mkdir -p /var/run/supervisor /var/log/supervisor /opt/bin

COPY src/main/resources/supervisord.conf /etc/
COPY src/main/resources/config.yaml ${CONFIG_FILE}
COPY src/main/resources/entry_point.sh /opt/bin/
COPY src/main/resources/webdav.sh /opt/bin/

RUN chmod +x /opt/bin/*.sh

ENTRYPOINT ["/bin/sh", "/opt/bin/entry_point.sh"]

RUN mkdir -p ${ROOT_PATH}

EXPOSE ${SERVER_PORT}