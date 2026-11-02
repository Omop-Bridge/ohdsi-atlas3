# syntax=docker/dockerfile:1.7

# Atlas3 WebAPI image with an overridden trexsql plugin jar.
#
# The upstream ghcr.io/ohdsi/webapi:3.0.0 image bakes a trexsql jar into
# /opt/webapi/plugins/trexsql.jar. This Dockerfile replaces it with a
# specific release downloaded from the OHDSI/trex GitHub releases page.

FROM ghcr.io/ohdsi/webapi:3.0.0

ARG TREXSQL_VERSION=0.3.3
ARG TREXSQL_URL=https://github.com/OHDSI/trex/releases/download/v${TREXSQL_VERSION}/trexsql-${TREXSQL_VERSION}.jar

USER root
RUN set -eux; \
    curl -fsSL -o /opt/webapi/plugins/trexsql.jar "${TREXSQL_URL}"; \
    unzip -p /opt/webapi/plugins/trexsql.jar META-INF/MANIFEST.MF > /tmp/trexsql.manifest; \
    grep -E '^Main-Class:[[:space:]]*trexsql\.core[[:space:]]*$' /tmp/trexsql.manifest > /dev/null; \
    rm /tmp/trexsql.manifest

LABEL org.atlas3.trexsql.version="${TREXSQL_VERSION}"
LABEL org.atlas3.webapi.base="ghcr.io/ohdsi/webapi:3.0.0"