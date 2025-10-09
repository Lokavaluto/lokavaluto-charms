FROM docker.0k.io/alpine:3.22.0 AS builder

RUN apk add --no-cache uv gcc python3-dev musl-dev linux-headers git

RUN uv venv

ENV PYC3L_CLI_VERSION=0.6.0

RUN cd /tmp && \
    git clone https://github.com/com-chain/pyc3l-cli.git && \
    cd pyc3l-cli && \
    git checkout "$PYC3L_CLI_VERSION" && \
    uv export -o requirements.txt --locked && \
    uv pip install -r requirements.txt && \
    uv pip  install .

FROM docker.0k.io/alpine:3.22.0

RUN apk add --no-cache python3

COPY --from=builder /.venv /.venv
ENV VIRTUAL_ENV=/.venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

ENTRYPOINT ["pyc3l"]
