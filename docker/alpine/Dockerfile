FROM brjsfn/alpine:bash
ENV IMG=alpine
ENV TAG=doxypypy1

RUN apk update && \
    apk upgrade && \
    apk add \
    	doxygen \
    	py3-pip \
    	git \
    	curl \
    	make \
    	graphviz

RUN pip3 install doxypypy

RUN git clone https://github.com/jothepro/doxygen-awesome-css.git /doxygen-awesome-css

WORKDIR /doxygen-awesome-css

RUN make install

WORKDIR /

COPY py_filter /usr/local/bin/py_filter

RUN mkdir code

RUN cp /doxygen-awesome-css/doxygen-awesome.css /code/

CMD ["/bin/bash"]
