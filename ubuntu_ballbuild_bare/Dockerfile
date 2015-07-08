# BALL Build Docker Image, by H.-Philipp Brachvogel 07.07.2015

FROM ubuntu:14.04

RUN apt-get -y update
RUN apt-get -y upgrade

RUN apt-get -y install git cmake gcc build-essential

# Install a basic SSH server
RUN apt-get install -y openssh-server
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd

RUN mkdir -p /var/run/sshd


# Install JDK 7 (latest edition)
RUN apt-get install -y openjdk-7-jdk


# Add user jenkins to the image
RUN adduser --quiet jenkins

RUN mkdir -p /home/jenkins/.ssh/
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA3o/4uemkSVdEN7DlMEsnX+BsT3nCpUPIgOE/6bFmnu1W4Dek4S9MWcey/+Tk690EYQDfM1EjQ/T0+Ezl7seTQCLGe0X+J5Vi82eVOARn2Gvc3fc20EKzCIAlRoT63c5ncvjy1jHk9+TYzS3ZQQMSSMMb3CPx6tFqcu5TYnrpNASNlg0wY7y/0v0Ww/sCMBvYJ+ZbJ+7P8cMOI+brOfq+2ItMdnOA5joHerwwWSADRpsYH4Mq4Do898SbH6G6BnPOctfM02RFCKoQtQmhuY0oYBZ0qqePhTPOVwFITUW2dcVhnIgYFtrVrREcyCb6LHuq1EkpcuNZVZLlBrDt0aKD0w== root@abibuilder0" > /home/jenkins/.ssh/authorized_keys

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
