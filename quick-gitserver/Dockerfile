FROM debian:latest
MAINTAINER Ravi Surulikamu <sravi.in@gmail.com>

ENV HOME /home/git
RUN apt-get update && apt-get install -y \
	git \
	openssh-server \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
	&& /etc/init.d/ssh start \
	&& /etc/init.d/ssh stop \
	&& useradd --create-home --home-dir $HOME \
	--shell /usr/bin/git-shell git \
	&& mkdir -p $HOME/.ssh $HOME/project.git \
	$HOME/git-shell-commands \
	&& git init --bare $HOME/project.git

COPY authorized_keys $HOME/.ssh/authorized_keys

RUN chmod -R go= $HOME/.ssh \
	&& chown -R git:git $HOME

WORKDIR $HOME
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
