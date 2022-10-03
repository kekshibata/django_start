ARG PYTHON_VERSION=3.9-slim-bullseye
ARG BUILD_ENVIRONMENT=production

FROM python:${PYTHON_VERSION}

RUN pip install --upgrade pip

COPY ./requirements .
RUN pip install -r ${BUILD_ENVIRONMENT}.txt

COPY --chown=django:django ./src /app

WORKDIR /app

RUN addgroup --system django \
    && adduser --system --ingroup django django

COPY --chown=django:django ./compose/production/django/entrypoint /entrypoint
RUN sed -i 's/\r$//g' /entrypoint
RUN chmod +x /entrypoint

RUN chown django:django /app

USER django

ENTRYPOINT ["/entrypoint"]
