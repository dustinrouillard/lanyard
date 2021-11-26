FROM elixir:1.12-alpine

ENV MIX_ENV=prod

COPY .git .git
COPY lib lib
COPY config config

COPY mix.exs .
COPY mix.lock .

RUN apk add openssl git openssh

RUN mix local.rebar --force \
    && mix local.hex --force \
    && mix deps.get

ENTRYPOINT [ "sh", "-c", "elixir --name lanyard@127.0.0.1 --cookie lanyard --no-halt -S mix" ]