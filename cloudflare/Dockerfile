FROM alpine:3.9

# ustc mirrors, it make `apk add` faster in china.
RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.9/main/" > /etc/apk/repositories && \
    echo "http://mirrors.ustc.edu.cn/alpine/v3.9/community/" >> /etc/apk/repositories && \
    apk add --no-cache --virtual .build-deps gcc g++ make musl-dev zlib-dev git openssl-dev && \
    cd /tmp && \
    wget https://fallabs.com/kyotocabinet/pkg/kyotocabinet-1.2.77.tar.gz && \
    tar xf kyotocabinet-1.2.77.tar.gz && \
    cd kyotocabinet-1.2.77 && ./configure && make -j$(nproc) && make install && cd .. && \
    git clone https://github.com/cloudflarearchive/kyototycoon.git && \
    cd kyototycoon && \
    ./configure --enable-static --disable-shared && \
    make -j$(nproc) && make install && cd .. && \
    cd kyotocabinet-1.2.77 && make uninstall && cd .. && \
    rm -rf kyotocabinet* kyototycoon* && \
    apk del .build-deps

EXPOSE 1978

CMD ["ktserver"]

