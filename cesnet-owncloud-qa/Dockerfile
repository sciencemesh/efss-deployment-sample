FROM owncloud/php:20.04 AS sciencemesh-builder

# Build the latest DEV version of the sciencemesh app
RUN apt update && apt install -y make git nodejs npm patch
RUN mkdir /tmp/build
RUN git clone https://github.com/pondersource/oc-sciencemesh.git /tmp/build/sciencemesh
WORKDIR /tmp/build/sciencemesh
COPY Makefile.diff /tmp/Makefile.diff
RUN patch -p0 < /tmp/Makefile.diff

RUN make
RUN make dist
WORKDIR /tmp/build/sciencemesh/build/artifacts/appstore/
RUN tar -xzf sciencemesh.tar.gz

FROM owncloud/server:10.10 AS server
WORKDIR /var/www/owncloud

# Apply the sciencemesh sharing patch && install the app
RUN apt update && apt install -y patch
RUN curl -sL https://patch-diff.githubusercontent.com/raw/owncloud/core/pull/40577.diff | patch -p1 -t --forward --no-backup-if-mismatch || true
RUN apt remove -y patch && apt autoremove
COPY --from=sciencemesh-builder /tmp/build/sciencemesh/build/artifacts/appstore/sciencemesh ./apps/sciencemesh

# Cleanup & re-set correct permissions
RUN find /var/www/owncloud \( \! -user www-data -o \! -group root \) -print0 | xargs -r -0 chown www-data:root
WORKDIR /var/www/owncloud
