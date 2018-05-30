FROM centos:7
WORKDIR /
RUN yum group install "Development Tools" -y
RUN yum install git wget tar zlib-devel -y
RUN git clone --recursive https://github.com/jts/nanopolish.git
WORKDIR /nanopolish
RUN make all

FROM busybox:glibc
COPY --from=0 /nanopolish/nanopolish* nanopolish/
COPY --from=0 /lib64/libz.so.1 \
            /lib64/librt.so.1 \
            /lib64/libdl.so.2 \
            /lib64/libstdc++.so.6 \
            /lib64/libgomp.so.1 \
            /lib64/libgcc_s.so.1 \
            /lib64/
ENTRYPOINT ["/nanopolish/nanopolish"]
