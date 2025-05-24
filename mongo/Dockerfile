FROM ubuntu:16.04

# Install MongoDB dependencies and SSH
RUN apt-get update && \
    apt-get install -y gnupg wget openssh-server && \
    mkdir /var/run/sshd

# Add MongoDB 5.0 repository and install MongoDB
RUN wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | apt-key add - && \
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/5.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-5.0.list && \
    apt-get update && \
    apt-get install -y mongodb-org

# Set up MongoDB data directory
RUN mkdir -p /data/db

# Set up SSH: set root password and allow root login
RUN echo 'root:rootpassword' | chpasswd && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Expose MongoDB and SSH ports
EXPOSE 27017 22

# Start both MongoDB and SSH when the container launches
CMD service mongod start && /usr/sbin/sshd -D
