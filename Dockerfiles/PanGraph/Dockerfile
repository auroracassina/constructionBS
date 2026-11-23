FROM rust:1.86-slim@sha256:57d415bbd61ce11e2d5f73de068103c7bd9f3188dc132c97cef4a8f62989e944

RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    cmake \
    pkg-config \
    zlib1g-dev \
    clang \
    libclang-dev \
    time \
    bash \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/neherlab/pangraph.git /pangraph
WORKDIR /pangraph
RUN git checkout cd1d4bd5b734ed67adedcf4dbea4fe365fa7c354
RUN cargo build --release --locked --bin pangraph
RUN cp target/release/pangraph /usr/local/bin/

RUN mkdir -p /results /input_data

CMD ["/bin/bash"]
