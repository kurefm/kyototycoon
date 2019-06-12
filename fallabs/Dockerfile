FROM alpine:3.8

COPY kyototycoon-0.9.56.patch /tmp/kyototycoon-0.9.56.patch

# ustc mirrors, it make `apk add` faster in china.
RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.8/main/" > /etc/apk/repositories && \
    echo "http://mirrors.ustc.edu.cn/alpine/v3.8/community/" >> /etc/apk/repositories && \
    apk add --no-cache --virtual .build-deps gcc g++ make musl-dev zlib-dev && \
    cd /tmp && \
    wget https://fallabs.com/kyotocabinet/pkg/kyotocabinet-1.2.77.tar.gz && \
    tar xf kyotocabinet-1.2.77.tar.gz && \
    cd kyotocabinet-1.2.77 && ./configure && make && make install && cd .. && \
    wget https://fallabs.com/kyototycoon/pkg/kyototycoon-0.9.56.tar.gz && \
    tar xf kyototycoon-0.9.56.tar.gz && \
    cd kyototycoon-0.9.56 && \
    ./configure --enable-static --disable-shared  && \
    patch < /tmp/kyototycoon-0.9.56.patch && \
    make && make install && cd .. && \
    cd kyotocabinet-1.2.77 && make uninstall && cd .. && \
    rm -rf kyotocabinet-1.2.77* kyototycoon-0.9.56* && \
    apk del .build-deps

EXPOSE 1978

CMD ["ktserver"]

