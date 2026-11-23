FROM ubuntu:22.04@sha256:0e0a0fc6d18feda9db1590da249ac93e8d5abfea8f4c3c0c849ce512b5ef8982

RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    cmake \
    time \
    bash \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/medvedevgroup/TwoPaCo.git /twopaco
WORKDIR /twopaco
RUN git checkout 7e859954211ea98a3f1e00c6a644fe29b43fe97b
RUN mkdir build && cd build && cmake ../src && make
RUN find /twopaco/build -type f \( -name twopaco -o -name graphdump \) -exec cp {} /usr/local/bin/ \;

RUN mkdir -p /results /input_data

CMD ["/bin/bash"]
