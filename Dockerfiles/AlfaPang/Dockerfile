FROM ubuntu:22.04@sha256:0e0a0fc6d18feda9db1590da249ac93e8d5abfea8f4c3c0c849ce512b5ef8982

RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    cmake \
    zlib1g-dev \
    time \
    bash \
    && rm -rf /var/lib/apt/lists/*

RUN git clone --recursive https://github.com/AdamCicherski/AlfaPang.git /alfapang
WORKDIR /alfapang
RUN git checkout f481a1b539fdfe0dddb7e83bc9a274290c37e8d5
RUN git submodule update --init --recursive
RUN mkdir build && cd build && cmake .. && cmake --build .

RUN mkdir -p /results /input_data

ENV PATH="/alfapang/build:${PATH}"

CMD ["/bin/bash"]
