FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y sshpass && \
    apt-get install -y openssh-server sudo python3 && \
    mkdir /var/run/sshd && \ 
    echo "root:ansible" | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]