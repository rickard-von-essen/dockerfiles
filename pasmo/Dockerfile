FROM debian:10 AS BUILD

ARG VERSION=0.6.0.20070113.0
ARG BUILD_DEPS="wget patch gcc make g++ bison"

COPY pasmo/pasmo.patch /tmp/pasmo.patch

RUN apt-get update && \
  apt-get install -y $BUILD_DEPS && \
  wget -O /tmp/pasmo-$VERSION.tgz http://pasmo.speccy.org/bin/pasmo-$VERSION.tgz && \
  tar -xz -C /tmp -f /tmp/pasmo-$VERSION.tgz && \
  cd /tmp/pasmo-$VERSION && \
  patch -p1 < /tmp/pasmo.patch && \
  ./configure && \
  make install

FROM debian:10

COPY --from=build /usr/local/bin/pasmo /usr/local/bin
