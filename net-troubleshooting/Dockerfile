FROM alpine:latest
LABEL tiagocorreia.netdebug.alpine.version=v1.0
RUN apk update \
&& apk upgrade \
&& apk add netcat-openbsd \
&& apk add nmap \
&& apk add curl \
&& apk add iputils \
&& apk add tcpdump \
&& apk add nginx \
&& apk add openssh \
&& apk add hping3 --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
&& apk add bind-tools \
&& curl -L "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" -o /usr/local/bin/kubectl \
&& chmod +x /usr/local/bin/kubectl

RUN echo 'This netdebug container has these tools available: [netcat-openbsd, nmap, curl, iputils, tcpdump, nginx, openssh , hping3, kubectl]' 

CMD ["/bin/sh"]
