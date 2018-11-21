FROM gcr.io/google-appengine/debian9
ENV ALERTMANAGER_VERSION 0.15.3

ENV ALERTMANAGER_URL="https://github.com/prometheus/alertmanager/releases/download/v$ALERTMANAGER_VERSION/alertmanager-$ALERTMANAGER_VERSION.linux-amd64.tar.gz"
ENV ALERTMANAGER_SHA256 b43fd8aba978f19375e37fb7924bcdc7dd45659b1b0f87a2815860001f100f46

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
