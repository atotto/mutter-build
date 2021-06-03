FROM ubuntu:groovy as builder
ENV DEBIAN_FRONTEND=noninteractive
COPY apt/sources.list /etc/apt/sources.list

RUN apt-get update && \
    apt-get build-dep -y mutter && \
    apt-get install -y devscripts && \
	mkdir build && cd build && apt-get source mutter && \
	rm -rf /var/lib/apt/lists/*
RUN cd build/mutter-* && \
    sed -i 's|case XkbNewKeyboardNotify:|//case XkbNewKeyboardNotify:|' ./src/backends/x11/meta-backend-x11.c && \
    dch --local + "Workaround https://gitlab.gnome.org/GNOME/gnome-shell/-/issues/1858" && \
    dch --release "" && \
    dpkg-buildpackage -rfakeroot -uc -b

FROM ubuntu:groovy
COPY --from=builder /build/libmutter-* /

