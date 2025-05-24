FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y gnupg wget openssh-server && \
    mkdir /var/run/sshd

RUN wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | apt-key add - && \
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/5.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-5.0.list && \
    apt-get update && \
    apt-get install -y mongodb-org

RUN mkdir -p /data/db

COPY wizexercise.txt /wizexercise.txt

RUN echo 'root:rootpassword' | chpasswd && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

EXPOSE 27017 22

CMD service mongod start && /usr/sbin/sshd -D
