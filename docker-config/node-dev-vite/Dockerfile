FROM nystudio107/node-dev-base:16-alpine

WORKDIR /var/www/project/

COPY ./npm_install.sh .
RUN chmod a+x npm_install.sh

# Install packages
RUN set -eux; \
    # Packages to install
    apk add --no-cache \
        git \
    && \
    # Clean out directories that don't need to be part of the image
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Run our webpack build in debug mode

# We'd normally use `npm ci` here, but by using `install`:
# - If `package-lock.json` is present, it will install what is in the lock file
# - If `package-lock.json` is missing, it will update to the latest dependencies
#   and create the `package-lock-json` file
# This automatic running adds to the startup overhead of `docker-compose up`
# but saves far more time in not having to deal with out of sync versions
# when working with teams or multiple environments
CMD ./npm_install.sh \
    && \
    cd /var/www/project/buildchain/ \
    && \
    npm run dev
