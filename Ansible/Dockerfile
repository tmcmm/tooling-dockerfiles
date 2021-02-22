FROM alpine:latest

LABEL Tiago Mendes <tiagomendes93@hotmail.com>
ARG ANSIBLE_VERSION="2.9.6"

#RUN apk --update add py-pip
#RUN apk add --no-cache python3 py-cryptography && \
#    apk add --no-cache --virtual python3-dev libffi-dev openssl-dev make gcc libc-dev make musl-dev && \
#    pip install ansible && \
#    pip install cryptography && \
#    pip install 'ansible[azure]' 

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
    pip3 install ansible[azure] pywinrm>=0.2.2 ;\
    #pip3 install --no-cache --upgrade setuptools wheel ansible==${ANSIBLE_VERSION} ;\
    apk del --no-cache --purge .build-deps ;\
    rm -rf /var/cache/apk/* ;\
    rm -rf /root/.cache ;

RUN ansible-galaxy install azure.azure_preview_modules   
RUN wget -nv -q https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt
RUN pip3 install -r requirements-azure.txt ;\
rm requirements-azure.txt

#RUN apk add --no-cache python3 py-cryptography && \
#    apk add --no-cache -

#RUN pip3 install 'ansible[azure]'
#RUN ansible-galaxy install azure.azure_preview_modules

#COPY ./linux/ansible/ansible*  /usr/local/bin/
#RUN chmod 755 /usr/local/bin/ansible* && \
#    pip3 install virtualenv && \
#    cd /opt \
#    virtualenv -p python3 ansible 
#RUN pip3 install pywinrm>=0.2.2
#RUN pip3 install ansible
#RUN pip3 install pywinrm>=0.2.2  ;\
#    pip3 install ansible[azure]
# RUN ansible-galaxy install azure.azure_preview_modules    
#    pip install 'ansible[azure]'


#RUN wget -nv -q https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt && \
#pip3 install -r requirements-azure.txt && \
#rm requirements-azure.txt
#RUN ansible-galaxy collection install azure.azcollection

# Temp: fix ansible modules. Proper fix is to update base layer to use regular python for Ansible.
#RUN wget -nv -q https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt \
#    && /opt/ansible/bin/python -m pip install -r requirements-azure.txt \
#    && rm requirements-azure.txt
#RUN ansible-galaxy collection install azure.azcollection
