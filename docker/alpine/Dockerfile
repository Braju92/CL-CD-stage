# Base image: brjsfn/alpine:bash
FROM brjsfn/alpine:bash

# Set environment variables IMG and TAG, used only to extract image name and tag from the Dockerfile
ENV IMG=alpine
ENV TAG=doxypypy-automation

# Update the package manager and install required packages
# Install doxygen for automatic documentation generation
# Install Python package manager, Git for version control, curl for data transfer, make for automation of program compilation, graphviz for diagram visualization
RUN apk update && \
    apk upgrade && \
    apk add \
    	doxygen \
    	py3-pip \
    	git \
    	curl \
    	make \
    	graphviz

# Install doxypypy Python package using pip3
RUN pip3 install doxypypy

# Clone the doxygen-awesome-css repository from GitHub into /doxygen-awesome-css directory
RUN git clone https://github.com/jothepro/doxygen-awesome-css.git /doxygen-awesome-css

# Install additional packages for graphviz, font rendering, and fonts for Ghostscript, this step is necessary cause from graphviz 3.10 to 3.11 Pango has been upgraded and in that upgrade from Pango 1.42 to 1.44 Pango removed support for bitmap fonts
RUN apk add --update graphviz font-bitstream-type1 ghostscript-fonts ttf-cantarell

# Set working directory to /doxygen-awesome-css
WORKDIR /doxygen-awesome-css

# Run 'make install' command within the current working directory
RUN make install

# Reset working directory to root
WORKDIR /

# Copy 'py_filter' file to /usr/local/bin/py_filter, py_filter is mandatory for doxygen to interpretate python code.
COPY py_filter /usr/local/bin/py_filter

# Create 'code' directory
RUN mkdir code

# Copy doxygen-awesome.css file from /doxygen-awesome-css to /code/
RUN cp /doxygen-awesome-css/doxygen-awesome.css /code/

# Set the default command to run '/bin/bash' shell
CMD ["/bin/bash"]
