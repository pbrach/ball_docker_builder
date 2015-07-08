# BALL Build Docker Image, by H.-Philipp Brachvogel 07.07.2015

FROM centos:6

RUN yum -y update
RUN yum -y upgrade

RUN yum -y groupinstall 'Development Tools' 
RUN yum -y install cmake

# Install a basic SSH server
RUN yum install -y openssh-server


# Install JDK 7 (latest edition)
RUN yum install -y java-1.7.0-openjdk


# Add user jenkins to the image
RUN adduser jenkins
# Set password for the jenkins user (you may want to alter this).
RUN echo "jenkins:jenkins" | chpasswd


RUN rm -f /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_rsa_key && \
ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key && \
ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key && \
sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && \
sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config

RUN mkdir -p /home/jenkins/.ssh/
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA3o/4uemkSVdEN7DlMEsnX+BsT3nCpUPIgOE/6bFmnu1W4Dek4S9MWcey/+Tk690EYQDfM1EjQ/T0+Ezl7seTQCLGe0X+J5Vi82eVOARn2Gvc3fc20EKzCIAlRoT63c5ncvjy1jHk9+TYzS3ZQQMSSMMb3CPx6tFqcu5TYnrpNASNlg0wY7y/0v0Ww/sCMBvYJ+ZbJ+7P8cMOI+brOfq+2ItMdnOA5joHerwwWSADRpsYH4Mq4Do898SbH6G6BnPOctfM02RFCKoQtQmhuY0oYBZ0qqePhTPOVwFITUW2dcVhnIgYFtrVrREcyCb6LHuq1EkpcuNZVZLlBrDt0aKD0w== root@abibuilder0" > /home/jenkins/.ssh/authorized_keys

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

