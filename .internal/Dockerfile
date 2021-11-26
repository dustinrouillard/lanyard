FROM elixir:1.12-alpine

WORKDIR /usr/src/lanyard

ENV MIX_ENV=prod

COPY .git .git
COPY lib lib
COPY config config

COPY mix.exs .
COPY mix.lock .

RUN apk add openssl git openssh

RUN git config --global url."git@github.com:".insteadOf https://github.com/
RUN git config --global url."git://".insteadOf https://
RUN ssh-keyscan -H github.com >> ~/.ssh/known_hosts

RUN mix local.rebar --force \
    && mix local.hex --force \
    && mix deps.get

ENTRYPOINT [ "sh", "-c", "elixir --name lanyard@0.0.0.0 --cookie lanyard --no-halt -S mix" ]