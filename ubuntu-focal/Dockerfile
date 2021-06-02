FROM ubuntu:focal as builder

ENV DEBIAN_FRONTEND=noninteractive

COPY apt/sources.list /etc/apt/sources.list

RUN apt-get update && \
    apt-get build-dep -y mutter && \
	mkdir build && cd build && apt-get source mutter && \
	rm -rf /var/lib/apt/lists/* && \
    cd mutter-* && \
    sed -i 's|case XkbNewKeyboardNotify:|//case XkbNewKeyboardNotify:|' ./src/backends/x11/meta-backend-x11.c && \
    dpkg-buildpackage -rfakeroot -uc -b

FROM ubuntu:focal

COPY --from=builder /build/libmutter-* /

