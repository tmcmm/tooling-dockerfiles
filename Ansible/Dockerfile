FROM alpine:latest

LABEL Tiago Mendes <tiagomendes93@hotmail.com>
ARG ANSIBLE_VERSION="2.10.7"

RUN apk --update add py-pip ;\
   apk add --no-cache --update --virtual .build-deps g++ python3-dev build-base libffi-dev openssl-dev gcc libc-dev make musl-dev;\
   apk add --no-cache python3 ca-certificates py-cryptography ;\
   if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi ;\
   echo "**** install pip ****" ;\
   python3 -m ensurepip ;\
   rm -r /usr/lib/python*/ensurepip ;\
   if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi ;\
   pip3 install --no-cache --upgrade pip ;\
   pip3 install --no-cache --upgrade setuptools wheel ansible==${ANSIBLE_VERSION} ;\
   #pip3 install ansible[azure] pywinrm>=0.2.2 ;\
   pip3 install --no-cache --upgrade setuptools wheel ansible==${ANSIBLE_VERSION} ;\
   apk del --no-cache --purge .build-deps ;\
   rm -rf /var/cache/apk/* ;\
   rm -rf /root/.cache ;

#RUN wget -nv -q https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt
#RUN pip3 install -r requirements-azure.txt ;
RUN ansible-galaxy install azure.azure_preview_modules
RUN ansible-galaxy collection install azure.azcollection --force

#RUN wget -nv -q https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt
#RUN pip3 install -r requirements-azure.txt ;\
#rm requirements-azure.txt
#RUN ansible-galaxy collection install azure.azcollection --force

#RUN ansible-galaxy collection install community.azure
#RUN ansible-galaxy collection install community.kubernetes
#RUN ansible-galaxy install azure.azure_preview_modules
