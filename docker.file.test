FROM centos:centos7.4.1708

MAINTAINER "ivan" co.tran@paradiseio.com

ENV container docker

RUN yum update -y glibc-common

RUN yum install -y --skip-broken sudo openssh-server openssh-clients tar screen crontabs strace telnet perl libpcap bc patch ntp dnsmasq unzip pax which
#RUN yum install -y sudo openssh-server openssh-clients

RUN yum install -y epel-release

#RUN yum install -y lsyncd sshpass rng-tools
RUN yum install -y sshpass

RUN useradd devops
RUN usermod -G wheel devops

RUN mkdir /home/devops/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA4V99CzDT+LZBFlyj84vLnnFMabJHfmiNPf6cmzHD+P2gfc/m1dzVwIIHYxnA54Y5TeoHqvegnYvOMt02TClwh6LIoabbRlOeW4MaBHh+rEs/i+T4mCcL7NEk82xkg61SFXphdBDCDfbidtTcfg+fdFAk1yA7GHhlO6WTkSB4RR1AMoarJNPpLXLGwtR0Y/fMrItQhNz2XKV21oTkwZn6X6TAKBiUaTEKMSGeHW5Jc4jG3qVqup723HbNd3KKTWkoWXI2IrhcTVx86laDo9xzunpHiJNrpWAV2McKJVEDa1t3RBEd7JhH6/2b9KKuLE7X4jMailhqZkDl8XR9/BICRQ== rsa 2048-042717" > /home/devops/.ssh/authorized_keys

RUN chown -R devops:devops /home/devops/.ssh
RUN chown -R devops:devops /home/devops/.ssh/authorized_keys

RUN chmod 700 /home/devops
RUN chmod 700 /home/devops/.ssh
RUN chmod 600 /home/devops/.ssh/authorized_keys


RUN sed -i "/%wheel/d" /etc/sudoers
RUN echo "%wheel  ALL=(ALL)       NOPASSWD: ALL" >> /etc/sudoers
RUN sed -i "/Defaults requiretty/d" /etc/sudoers
RUN sed -i "/Defaults    requiretty/d" /etc/sudoers

RUN sed -i "/UseDNS/d" /etc/ssh/sshd_config
RUN echo "UseDNS no" >> /etc/ssh/sshd_config

RUN sed -i "/PasswordAuthentication yes/d" /etc/ssh/sshd_config
RUN echo "PasswordAuthentication no" >> /etc/ssh/sshd_config

RUN echo "sshd:45.32.100.87" > /etc/hosts.allow
RUN echo "sshd:114.34.2.95" >> /etc/hosts.allow
RUN echo "sshd:45.76.202.152" >> /etc/hosts.allow
RUN echo "sshd:35.236.183.125" >> /etc/hosts.allow
RUN echo "sshd:14.161.36.28" >> /etc/hosts.allow
RUN echo "sshd:172.245.47.13" >> /etc/hosts.allow
RUN echo "sshd:35.200.81.193" >> /etc/hosts.allow
RUN echo "sshd:14.161.12.30" >> /etc/hosts.allow
RUN echo "sshd:all" > /etc/hosts.deny

RUN echo  "SELINUX=disabled" > /etc/selinux/config
RUN echo "SELINUXTYPE=targeted" >> /etc/selinux/config

RUN echo "* hard nproc 65535" > /etc/security/limits.conf
RUN echo "* hard nofile 65535" >> /etc/security/limits.conf
RUN echo "* soft nofile 65535" >> /etc/security/limits.conf
RUN echo "* soft nproc 65535" >> /etc/security/limits.conf

#systemctl restart sshd.service

RUN yum install epel-release -y
RUN yum install libselinux-python rsync -y
RUN yum install selinux-policy-targeted -y
RUN touch /.autorelabel

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in ; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done);
#RUN rm -f /lib/systemd/system/multi-user.target.wants/;
RUN rm -f /etc/systemd/system/.wants/;
#RUN rm -f /lib/systemd/system/local-fs.target.wants/;
RUN rm -f /lib/systemd/system/sockets.target.wants/udev;
RUN rm -f /lib/systemd/system/sockets.target.wants/initctl;
#RUN rm -f /lib/systemd/system/basic.target.wants/;
RUN rm -f /lib/systemd/system/anaconda.target.wants/*;

EXPOSE 80
EXPOSE 443
EXPOSE 22

CMD ["/usr/sbin/init"]
