FROM ${dockerfile.based.image}
LABEL authors="Happy TestOps <contact@ndviet.org>"
LABEL application="WsgiDAV ${wsgidav.version}"

#======================================
# Add ENV
#======================================
ENV PIP_ROOT_USER_ACTION=ignore
ENV CONFIG_FILE config.yaml
ENV ROOT_PATH /share
ENV SERVER cheroot
ENV HOST 0.0.0.0
ENV SERVER_PORT 8080

#======================================
# Add dependencies
#======================================
RUN apk add --no-cache --virtual .build-deps gcc libxslt-dev musl-dev py3-lxml py3-pip \
    && apk add --no-cache --virtual .build-deps supervisor bash \
    && python -m pip install --upgrade --no-cache-dir pip lxml \
    && pip install --upgrade --no-cache-dir ${SERVER} \
    && pip install --upgrade --no-cache-dir wsgidav==${wsgidav.version} \
    && rm -rf /tmp/* /var/cache/apk/*

#======================================
# Add Supervisor configuration files
#======================================
RUN  mkdir -p /var/run/supervisor /var/log/supervisor /opt/bin

COPY supervisord.conf /etc/
COPY config.yaml /opt/bin/${CONFIG_FILE}
COPY entry_point.sh /opt/bin/
COPY webdav.sh /opt/bin/

RUN chmod +x /opt/bin/*.sh

ENTRYPOINT ["/bin/sh", "/opt/bin/entry_point.sh"]

RUN mkdir -p ${ROOT_PATH}

EXPOSE ${SERVER_PORT}