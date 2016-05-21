# We need a proper OS
FROM debian:jessie

# Installation of specific version of Subversion
RUN apt-get update && \
    apt-get install -y subversion=1.8.10-6+deb8u4

# Creating a Subversion repository
RUN svnadmin create /opt/svnrepo

# Adding the Subversion auth files
RUN rm -rf /opt/svnrepo/conf
COPY conf/* /opt/svnrepo/conf/

# Standard SVN port
EXPOSE 3690

# Starts the SVN daemon
CMD ["svnserve", "--daemon", "--foreground", "--root", "/opt/svnrepo"]
