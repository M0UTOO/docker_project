# Créer un Dockerfile pour cette application en mode production

#ADD RUST NIGHTLY
FROM rustlang/rust:nightly AS build

#GET THE REQUIRE LIB
RUN apt update && apt install -y libpq-dev

#GET A WORKING PLACE
WORKDIR /blog

#GET THE APP FILES
COPY . ./

RUN cargo install --path ./

RUN cp /usr/local/cargo/bin/blog ./blog

#DOWNLOADING TOOLS
RUN cargo install diesel_cli --no-default-features --features postgres

#RUNS MIGRATIONS
CMD ["bash", "-c", "sleep 2 && diesel migration run && ./blog"]
