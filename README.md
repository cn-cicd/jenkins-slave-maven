# Jenkins Slave Maven [![Docker hub](https://img.shields.io/docker/pulls/jnonino/jenkins-slave-maven.svg)](https://hub.docker.com/r/jnonino/jenkins-slave-maven/)

Jenkins Slave for Maven builds. Docker image based on Maven official image.

	https://hub.docker.com/r/jnonino/jenkins-slave-maven/

## Tools Installed ##

- Maven
- Open Java JDK
- Git
- Subversion
- Mercurial
- wget
- curl
- unzip
- OpenSSH
- CA Certificates

## Add certificate to connect to HTTPS repositories

To add custom certificates and root CAs, create a new Dockerfile and import them with the following code.

	FROM jnonino/jenkins-slave-maven
	LABEL maintainer="Julian Nonino <noninojulian@gmail.com>"

	# Trust Root CA
	COPY Root_CA.crt /tmp
	RUN keytool -importcert -alias Root_CA -keystore ${JAVA_HOME}/jre/lib/security/cacerts -storepass changeit -file /tmp/Root_CA.crt -noprompt && \
		cp /tmp/Root_CA.crt /usr/local/share/ca-certificates/ && \
		chmod 644 /usr/local/share/ca-certificates/Root_CA.crt && \
		update-ca-certificates

	CMD ["/bin/bash"]
