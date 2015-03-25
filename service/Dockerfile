FROM ubuntu

RUN mkdir -p /root/a && \
    mkdir -p /root/b && \
    touch /root/a/a && \
    touch /root/b/b

CMD cd /root/$POOL && python3 -m http.server $PORT
