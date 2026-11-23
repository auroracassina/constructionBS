FROM rust:1.92-slim@sha256:bf3368a992915f128293ac76917ab6e561e4dda883273c8f5c9f6f8ea37a378e

RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    pkg-config \
    time \
    bash \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/pangenome/seqwish.git /seqwish
WORKDIR /seqwish
RUN git checkout 97d603f58ab792f2e92f33bce70130ddb70770e0
# Build for the host CPU, as release v0.7.12 did via .cargo/config.toml
ENV RUSTFLAGS="-C target-cpu=native"
RUN cargo build --release --locked
RUN cp target/release/seqwish /usr/local/bin/

RUN mkdir -p /results /input_data

CMD ["/bin/bash"]
