FROM gcr.io/google-appengine/debian9
ENV ALERTMANAGER_VERSION 0.23.0
ENV C2D_RELEASE=${ALERTMANAGER_VERSION}

ENV ALERTMANAGER_URL="https://github.com/prometheus/alertmanager/releases/download/v$ALERTMANAGER_VERSION/alertmanager-$ALERTMANAGER_VERSION.linux-amd64.tar.gz"
ENV ALERTMANAGER_SHA256 77793c4d9bb92be98f7525f8bc50cb8adb8c5de2e944d5500e90ab13918771fc

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
