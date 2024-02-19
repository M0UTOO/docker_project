# Créer un Dockerfile pour cette application en mode production

#ADD RUST NIGHTLY
FROM rustlang/rust:nightly AS build

#GET THE REQUIRE LIB
RUN apt update && apt install -y libpq-dev

#GET A WORKING PLACE
WORKDIR /blog

#ENV VARIABLES
ARG DATABASE_URL
ENV DATABASE_URL="postgres://thomas:admin@0.0.0.0:5432/blog"

ARG ROCKET_ADDRESS
ENV ROCKET_ADDRESS=${ROCKET_ADDRESS}

#GET THE APP FILES
COPY . ./


#CMD cargo install --path ./

#CMD cp /usr/local/cargo/bin/blog ./blog

#DOWNLOADING TOOLS
RUN cargo install diesel_cli --no-default-features --features postgres

#RUNS MIGRATIONS
RUN diesel migration run

#CMD ./blog 
RUN cargo run