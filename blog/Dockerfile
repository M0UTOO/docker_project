# Créer un Dockerfile pour cette application en mode production

#ADD RUST NIGHTLY
FROM rustlang/rust:nightly

#GET THE REQUIRE LIB
RUN apt update && apt install -y libpq-dev

#DOWNLOADING TOOLS
RUN cargo install diesel_cli --no-default-features --features postgres

#GET A WORKING PLACE
WORKDIR /blog

#GET THE APP FILES
COPY . ./

#PREPARE THE APP
RUN cargo install --path ./
RUN cp /usr/local/cargo/bin/blog ./blog

#RUNS MIGRATIONS AND THE APP    
RUN  diesel migration run
RUN  ./blog
