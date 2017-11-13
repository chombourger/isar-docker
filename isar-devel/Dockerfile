FROM debian 

# Install required packages
RUN apt-get -y update
RUN apt install -y		\
	command-not-found	\
	openssh-server		\
	git			\
	sudo			\
	vim

# Install packages required by Isar
RUN apt install -y		\
	binfmt-support		\
	dosfstools		\
	locales			\
	mtools			\
	multistrap		\
	parted			\
	python3			\
	qemu			\
	qemu-user-static	\
	reprepro

# Setup a "work" volume
RUN mkdir /work /var/run/sshd
VOLUME /work

# Clean-up apt cache to reclaim disk space
RUN apt purge

# Create a "docker" user (password is "docker")
RUN useradd -m "docker" -p "sDBIQEhq8Z7kY"
RUN chsh -s /bin/bash docker
RUN echo "docker ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/90-docker

# Configure locales
RUN echo "export LC_ALL=en_US.UTF-8" >>/home/docker/.bashrc
RUN echo "export LANG=en_US.UTF-8" >>/home/docker/.bashrc
RUN echo "export LANGUAGE=en_US:en" >>/home/docker/.bashrc
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen
RUN dpkg-reconfigure --frontend=noninteractive locales

# Setup SSH service
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
