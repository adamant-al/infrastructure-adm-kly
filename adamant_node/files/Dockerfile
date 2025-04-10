FROM node:22-bookworm

RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils  \
    bash \
    locales \
    libtool \
    mc \
    git \
    curl \
    python3 \
    build-essential \
    automake \
    autoconf \
    redis-server \
    wget \
    autotools-dev \
    libsodium-dev \
    postgresql \
    postgresql-contrib \
    libpq-dev \
    pkg-config

RUN useradd -m adamant

RUN service postgresql start && \
    su - postgres -c "psql -U postgres --command \"CREATE USER adamant WITH PASSWORD 'password';\"" && \
    su - postgres -c "psql -U postgres --command \"CREATE DATABASE adamant_test OWNER adamant;\"" && \
    su - postgres -c "psql -U postgres --command \"CREATE DATABASE adamant_main OWNER adamant;\"" && \
    service postgresql stop


USER root

WORKDIR /app
RUN git clone https://github.com/Adamant-im/adamant --branch=dev .

RUN npm install
RUN cp config.default.json config.json

EXPOSE 36666 36668 443 80

CMD ["sh", "-c", "service postgresql start && npm start"]
