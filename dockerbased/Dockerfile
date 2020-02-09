FROM ubuntu:16.04

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:Hola12345.' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

#Install ping
RUN apt-get -y update
RUN apt-get -y install iputils-ping

#Install vi
RUN apt-get -y install vim

#Install sshpass
RUN apt-get -y install sshpass


#Install ansible
RUN mkdir -p /home/ansible
WORKDIR /home/ansible
RUN apt-get -y install ansible
ARG name=ubuntuansible

COPY control-volume/ansible.cfg /etc/ansible/ansible.cfg

EXPOSE 22 80 8080
CMD ["/usr/sbin/sshd", "-D"]

# $ docker run -d -P --name uas ubuntuansiblessh
# $ docker port uas 22
# $ ssh root@localhost -p 32769
