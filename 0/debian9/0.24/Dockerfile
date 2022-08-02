FROM gcr.io/google-appengine/debian9
ENV ALERTMANAGER_VERSION 0.24.0
ENV C2D_RELEASE=${ALERTMANAGER_VERSION}

ENV ALERTMANAGER_URL="https://github.com/prometheus/alertmanager/releases/download/v$ALERTMANAGER_VERSION/alertmanager-$ALERTMANAGER_VERSION.linux-amd64.tar.gz"
ENV ALERTMANAGER_SHA256 6fa982232ae7be5524f5b3cd4e90b7c6a75086368200c917644eaa3e806555dc

RUN set -x && \
    apt-get update && apt-get install -qq -y wget && \
    mkdir -p /etc/alertmanager && \
    mkdir alertmanager-files && cd alertmanager-files && \
    wget -O alertmanager.tar.gz "$ALERTMANAGER_URL" && \
    echo "$ALERTMANAGER_SHA256 alertmanager.tar.gz" | sha256sum -c - && \
    tar xfvz alertmanager.tar.gz --strip-components=1 && \
    mv amtool          /bin/ && \
    mv alertmanager    /bin/ && \
    mkdir -p /usr/share/doc/alertmanager && \
    mv LICENSE /usr/share/doc/alertmanager/ && \
    mv alertmanager.yml /etc/alertmanager/alertmanager.yml && \
    cd - && \
    rm -r alertmanager-files

EXPOSE     9093
VOLUME     [ "/alertmanager" ]
WORKDIR    /etc/alertmanager
ENTRYPOINT [ "/bin/alertmanager" ]
CMD        [ "--storage.path=/alertmanager" ]
