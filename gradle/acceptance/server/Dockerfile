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

# Copying the file to commit
ADD project /opt/project/

# Preparing the repository trunk
RUN svn mkdir file:///opt/svnrepo/project/trunk --parents --message "Trunk"

# Checking out the trunk
RUN svn checkout --force file:///opt/svnrepo/project/trunk /opt/project

# Adding the files
RUN svn add /opt/project/*

# Commit
RUN svn commit /opt/project --message "Initial commit"

# Standard SVN port
EXPOSE 3690

# Starts the SVN daemon
CMD ["svnserve", "--daemon", "--foreground", "--root", "/opt/svnrepo"]
