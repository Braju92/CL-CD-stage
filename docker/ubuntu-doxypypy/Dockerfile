FROM ubuntu:latest

ENV IMG=ubuntu
ENV TAG=doxypypy


# Update the package lists and install doxygen, pip3, git, curl
RUN apt-get update && \
    apt-get install -y \
    	doxygen \
    	python3-pip \
    	git \
    	curl \
    	&& rm -rf /var/lib/apt/lists/*
    	
# Install doxypypy
RUN pip3 install doxypypy

# Clone doxygen-awesome-css repository
RUN git clone https://github.com/jothepro/doxygen-awesome-css.git /doxygen-awesome-css

# Change directory
WORKDIR /doxygen-awesome-css

# Install doxygen-awesome-css
RUN make install

# Change directory to root
WORKDIR /

# Copy py_filter into image
COPY py_filter /usr/local/bin/py_filter

RUN doxygen -w html header.html delete_me.html delete_me.css



