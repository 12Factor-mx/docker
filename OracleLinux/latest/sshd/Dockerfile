# LICENSE MIT
#
# Copyright (c) 2018 12factor and/or its affiliates and/or Miguel Jesús Díaz Macedo.
#
# Taken from https://docs.docker.com/engine/examples/running_ssh_service/ 
#            https://hub.docker.com/_/oraclelinux/
#
# Becuase of Ansible usage I extended the original Oracle's linux latest tagged version image (oraclelinux:latest) with an up and running sshd server


FROM oraclelinux:latest

MAINTAINER Miguel Jesús Díaz Macedo <webmaster@12factor.mx>


RUN yum install -y openssh openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN ssh-keygen -q -t rsa -N '' -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -q -t ecdsa -N '' -f /etc/ssh/ssh_host_ecdsa_key
RUN ssh-keygen -q -t ed25519 -N '' -f /etc/ssh/ssh_host_ed25519_key


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
