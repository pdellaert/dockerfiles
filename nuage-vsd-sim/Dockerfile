FROM python:2-alpine
ARG version=5.2.2
LABEL maintainer="Philippe Dellaert (philippe@dellaert.org)"
LABEL version=$version
LABEL description="This runs a Nuage VSD API simulator which can be used for basic testing of the Nuage API."

RUN apk --update add git && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*
RUN pip install --upgrade pip vspk==$version
RUN cd /tmp && \
    git clone https://github.com/pdellaert/monolithe.git && \
    cd monolithe && \
    git checkout vsd-sim && \
    pip install .
RUN cd /tmp && \
    git clone https://github.com/nuagenetworks/vsd-api-specifications && \
    cd vsd-api-specifications && \
    git checkout r$version
RUN cd /tmp && \
    monogen -f /tmp/vsd-api-specifications -c /tmp/monolithe/monolithe/generators/lang/vsdsim/vanilla/conf/monolithe.ini --generation-version $version -L vsdsim && \
    cd codegen/vsdsim && \
    pip install .
RUN rm -rf /tmp/codegen /tmp/monolithe /tmp/vsd-api-specifications

ENTRYPOINT ["nuage-vsd-sim"]
