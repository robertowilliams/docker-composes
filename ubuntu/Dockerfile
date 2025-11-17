FROM ubuntu:22.04

RUN apt update && apt install -y \
    openssh-server \
    sudo \
    nano \
    tree

# Create ssh directory
RUN mkdir /var/run/sshd

# Create user 'nalitica'
RUN useradd -ms /bin/bash nalitica && echo "nalitica:Psalm121@" | chpasswd && adduser nalitica sudo

# Set root password
RUN echo "root:Psalm121@" | chpasswd

# Enable root login via SSH
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/PermitRootLogin no/PermitRootLogin yes/' /etc/ssh/sshd_config

# Enable password authentication
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config
RUN sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Fix login issues
RUN sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
