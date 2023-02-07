FROM owncloud/php:20.04 AS sciencemesh-builder

# Build the latest DEV version of the sciencemesh app
RUN apt update && apt install -y make git nodejs npm patch
RUN mkdir /tmp/build
RUN git clone https://github.com/pondersource/oc-sciencemesh.git /tmp/build/sciencemesh
WORKDIR /tmp/build/sciencemesh
RUN ./release.sh
WORKDIR /tmp/build/sciencemesh/release
RUN tar -xzf sciencemesh.tar.gz

FROM owncloud/server:10.10 AS server
WORKDIR /var/www/owncloud

ADD ./10-configure_extras.sh /etc/post_install.d/10-configure_extras.sh
RUN chmod u+x -R /etc/post_install.d/

# Apply the sciencemesh sharing patch && install the app
RUN apt update && apt install -y patch
RUN curl -sL https://patch-diff.githubusercontent.com/raw/owncloud/core/pull/40577.diff | patch -p1 -t --forward --no-backup-if-mismatch || true
RUN apt remove -y patch && apt autoremove
COPY --from=sciencemesh-builder /tmp/build/sciencemesh/release/sciencemesh ./apps/sciencemesh

# Cleanup & re-set correct permissions
RUN find /var/www/owncloud \( \! -user www-data -o \! -group root \) -print0 | xargs -r -0 chown www-data:root
WORKDIR /var/www/owncloud
