FROM python:3.10-bullseye

ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

USER root

COPY ./ansible-kubespray/requirements.txt /etc/requirements.txt
COPY ./ansible-kubespray/requirements.yml /etc/requirements.yml


RUN wget https://releases.hashicorp.com/vault/1.17.5/vault_1.17.5_linux_amd64.zip

RUN unzip vault_1.17.5_linux_amd64.zip

RUN mv vault /usr/local/bin/


RUN pip3 install --upgrade pip; \
    python3 -m pip install -r /etc/requirements.txt;\
    ansible-galaxy collection install -r /etc/requirements.yml;\
    python3 -m pip install -r ~/.ansible/collections/ansible_collections/kubernetes/core/requirements.txt;\
    python3 -m pip install -r ~/.ansible/collections/ansible_collections/azure/azcollection/requirements.txt

CMD [ "/usr/sbin/init" ]