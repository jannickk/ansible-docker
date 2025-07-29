FROM python:3.13-bullseye


ARG ANSIBLE_VERSION

ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

USER root

RUN apt install wget
RUN apt install unzip


RUN wget https://releases.hashicorp.com/terraform/1.9.6/terraform_1.9.6_linux_amd64.zip

RUN unzip terraform_1.9.6_linux_amd64.zip

# Move the terraform binary to a directory in your system's PATH.
RUN mv terraform /usr/local/bin/

RUN pip3 install --upgrade pip; \
    python3 -m pip install ansible-core==${ANSIBLE_VERSION}

COPY ./ansible-terraform/requirements.txt /etc/requirements.txt
COPY ./ansible-terraform/requirements.yml /etc/requirements.yml

RUN pip3 install --upgrade pip; \
    python3 -m pip install -r /etc/requirements.txt;\
    ansible-galaxy collection install -r /etc/requirements.yml;\
    python3 -m pip install -r ~/.ansible/collections/ansible_collections/azure/azcollection/requirements.txt

CMD [ "/usr/sbin/init" ]

