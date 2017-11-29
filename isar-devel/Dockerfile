FROM debian 

COPY co-isar /usr/bin/co-isar

# Install required packages
# Start with base packages and continue with Isar dependencies
RUN 					\
	apt-get -y update		\
	&& apt install -y		\
		command-not-found	\
		dos2unix		\
		openssh-server		\
		git			\
		sudo			\
		vim			\
	&& apt install -y		\
		binfmt-support		\
		dosfstools		\
		locales			\
		mtools			\
		multistrap		\
		parted			\
		python3			\
		qemu			\
		qemu-user-static	\
		reprepro		\
	&& apt purge			\
	&& dos2unix /usr/bin/co-isar	\
	&& chmod 755 /usr/bin/co-isar

# Setup a "work" volume
RUN mkdir /work /var/run/sshd
VOLUME /work

# Create a "docker" user (password is "docker")
RUN						\
	useradd -m "docker" -p "sDBIQEhq8Z7kY"	\
	&& chsh -s /bin/bash docker		\
	&& echo "docker ALL=(ALL) NOPASSWD:ALL"	\
		>/etc/sudoers.d/90-docker

# Configure locales
RUN 									\
	echo "export LC_ALL=en_US.UTF-8" >>/home/docker/.bashrc		\
	&& echo "export LANG=en_US.UTF-8" >>/home/docker/.bashrc	\
	&& echo "export LANGUAGE=en_US:en" >>/home/docker/.bashrc	\
	&& sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/'		\
		/etc/locale.gen						\
	&& dpkg-reconfigure --frontend=noninteractive locales

# Setup SSH service
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
