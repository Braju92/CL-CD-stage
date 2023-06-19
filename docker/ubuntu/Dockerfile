FROM ubuntu:latest

ENV IMG=ubuntu
ENV TAG=common-features

# Update the package lists
RUN apt-get update

# Install common utilities
RUN apt-get install -y curl wget git unzip

# Install common networking tools
RUN apt-get install -y iputils-ping dnsutils net-tools

# Install common text editors
RUN apt-get install -y nano vim

# Install Python
RUN apt-get install -y python3 python3-pip

# Install Node.js and npm
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

# Install Java
RUN apt-get install -y default-jdk

# Clean up
RUN apt-get autoremove -y && apt-get clean
