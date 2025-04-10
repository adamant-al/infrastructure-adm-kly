ARG NODEJS_VERSION=18

##### Stage 1

FROM node:$NODEJS_VERSION-bookworm AS builder

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    python3 \
    libtool \
    autoconf \
    automake \
    rustc \
    cargo \
    cmake \
    clang \
    rustfmt \
    linux-headers-amd64 && \
    mkdir /build && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /build

COPY ./yarn.lock ./package.json ./.npmrc ./
RUN yarn install --frozen-lockfile


##### Stage 2

FROM node:$NODEJS_VERSION-bookworm

RUN mkdir /klayr && mkdir /klayr/.klayr

WORKDIR /klayr

COPY  ./ .
COPY --from=builder /build/node_modules/ ./node_modules/

RUN npm run build

ENTRYPOINT ["/klayr/bin/run"]
CMD ["start", "--network", "mainnet"]
