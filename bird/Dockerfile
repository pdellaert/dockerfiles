FROM alpine:edge
EXPOSE 179

LABEL maintainer="Philippe Dellaert (philippe@dellaert.org)"
LABEL description="A container running BIRD (https://bird.network.cz/)"

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing/" >> /etc/apk/repositories && \
    apk add --no-cache bird && \
    mkdir -p /etc/bird

ENTRYPOINT ["bird", "-c", "/etc/bird/bird.conf", "-d"]
