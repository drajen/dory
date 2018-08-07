FROM registry.access.redhat.com/rhel7.5
RUN yum install -y git make && \
    curl -o go.tar.gz https://dl.google.com/go/go1.10.3.linux-amd64.tar.gz && \
    tar xzvf go.tar.gz -C /usr/local && \
    git clone https://github.com/hpe-storage/dory go/src/github.com/hpe-storage/dory
ENV PATH=$PATH:/usr/local/go/bin
ENV GOPATH=/go
WORKDIR go/src/github.com/hpe-storage/dory
ADD Makefile Makefile
RUN make vendor && \
    make doryd 
RUN cp doryd /doryd && \
    yum remove -y git make && \
    yum autoremove -y && \
    rm -rf go /usr/local/go && \
    yum clean all && \
    rm -rf /var/cache/yum
ENTRYPOINT [ "doryd" ]
CMD [ "/etc/kubernetes/admin.conf", "dev.hpe.com" ]
