ARG ODOO_VERSION=14.0

FROM registry.git.veone.net/veone/odoo/ce:$ODOO_VERSION
LABEL vendor="veone/odoo/ee" maintainer="dev@veone.net" version="1.0.0"

USER root

SHELL ["/bin/bash", "-xo", "pipefail", "-c"]

# Install some deps, lessc and less-plugin-clean-css, and wkhtmltopdf
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        git=1:2.20.1-2+deb10u3 \
    && rm -rf /var/lib/apt/lists/*

ARG ODOO_USER
ARG ODOO_PASSWORD
ARG ODOO_VERSION=14.0

RUN set -ex && \
    mkdir -p /mnt/enterprise-addons \
    && git clone --depth 1 -b "${ODOO_VERSION}" "https://$ODOO_USER:$ODOO_PASSWORD@github.com/odoo/enterprise.git" /mnt/enterprise-addons

# Copy entrypoint script and Odoo configuration file
COPY ./docker/odoo.conf /etc/odoo/

# Set permissions on directory /mnt/enterprise-addons for users addons
RUN chown -R odoo /etc/odoo/odoo.conf /mnt/enterprise-addons

# Set default user when running the container
USER odoo
