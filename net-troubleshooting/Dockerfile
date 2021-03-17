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
&& apk add git \
&& apk add openssh \
#&& apk add conntrack \
&& apk add tcptraceroute \
&& apk add bc \
&& apk add hping3 --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
&& apk add bind-tools \
&& curl -L "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" -o /usr/local/bin/kubectl \
&& chmod +x /usr/local/bin/kubectl
RUN set -x; cd "$(mktemp -d)" ;\
  OS="$(uname | tr '[:upper:]' '[:lower:]')" ;\
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" ;\
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.tar.gz" ;\
  tar zxvf krew.tar.gz ;\
  KREW=./krew-"${OS}_${ARCH}" ;\
  "$KREW" install krew 

RUN export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"

# Install tcping
RUN wget http://www.vdberg.org/~richard/tcpping ;\
    sudo cp tcpping /usr/bin ;\
    sudo chmod 755 tcpping

RUN echo -e 'This netdebug container has these tools available: [netcat-openbsd, nmap, curl, iputils, tcpdump, nginx, openssh , hping3, kubectl, sniff, conntrack, tcping]' 
#ENTRYPOINT echo "This netdebug container has these tools available: [netcat-openbsd, nmap, curl, iputils, tcpdump, nginx, openssh , hping3, kubectl]"
CMD ["/bin/sh"]
