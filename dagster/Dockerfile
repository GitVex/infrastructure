# Image for the Dagster webserver and daemon. User code lives in its own image
# (ghcr.io/gitvex/hockey-pipelines) and is reached over gRPC, see workspace.yaml.
FROM python:3.12-slim

# dagster-* integration libraries are versioned 0.(minor+16).patch relative to core.
# dagster-postgres is built on psycopg2. SQLAlchemy 2.1 switched the default
# postgresql:// driver to psycopg 3, which leaves Dagster with closed connections,
# so stay on SQLAlchemy 2.0.
RUN pip install --no-cache-dir \
    dagster==1.13.29 \
    dagster-webserver==1.13.29 \
    dagster-postgres==0.29.29 \
    "sqlalchemy==2.0.57"

ENV DAGSTER_HOME=/opt/dagster/dagster_home/
RUN mkdir -p $DAGSTER_HOME
COPY dagster.yaml workspace.yaml $DAGSTER_HOME
WORKDIR $DAGSTER_HOME
