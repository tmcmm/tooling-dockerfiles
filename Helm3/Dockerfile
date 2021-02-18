FROM alpine:latest


LABEL maintainer="Tiago Mendes <tiagocorreia@microsoft.com>"

ENV KUBE_LATEST_VERSION="v1.18.3"
ENV HELM_VERSION="v3.3.4"

# Install requirements
RUN apk add --update ca-certificates \
    && apk add --update -t deps curl \
    && apk add --update gettext \
    && curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl \
    && apk del --purge deps \
    && rm /var/cache/apk/*

##### Notice: Install Helm #####
RUN apk add --update ca-certificates \
 && apk add --update -t deps wget \
 && wget -q https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz -O - | tar -xzO linux-amd64/helm > /usr/local/bin/helm \
 && chmod +x /usr/local/bin/helm \
 && chmod g+rwx /root \
 && mkdir /config \
 && chmod g+rwx /config \
 && helm repo add "stable" "https://charts.helm.sh/stable"



ENTRYPOINT []
CMD ["/bin/sh"]
