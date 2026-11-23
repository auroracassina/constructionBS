FROM rust:1.86-slim@sha256:57d415bbd61ce11e2d5f73de068103c7bd9f3188dc132c97cef4a8f62989e944

RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    zlib1g-dev \
    python3 \
    time \
    bash \
    && rm -rf /var/lib/apt/lists/*

# rust-mdbg
RUN git clone https://github.com/ekimb/rust-mdbg.git /rust-mdbg
WORKDIR /rust-mdbg
RUN git checkout 077083d4890e8570b642eff9b3e2c0aa488498b7
# Unused dependencies (only mentioned in comments) that no longer compile:
# - petgraph-graphml requires xml-rs 0.7, which was yanked from crates.io
# - bio (declared as "*") resolves to 4.2.2, which requires a newer Rust than 1.86
RUN sed -i -e '/^petgraph-graphml/d' -e '/^bio = /d' Cargo.toml
RUN cargo build --release

# gfatools (needed for graph simplification, used by magic_simplify)
RUN git clone https://github.com/lh3/gfatools.git /gfatools
WORKDIR /gfatools
RUN git checkout 39c54d5dfe4678d4cfb75b37bd27d4fb21f4de72
RUN make && cp gfatools /usr/local/bin/

# magic_simplify calls "python", but the image only has python3
RUN ln -s /usr/bin/python3 /usr/local/bin/python

WORKDIR /rust-mdbg
ENV PATH="/rust-mdbg/target/release:/rust-mdbg/utils:${PATH}"

RUN mkdir -p /results /input_data

CMD ["/bin/bash"]
