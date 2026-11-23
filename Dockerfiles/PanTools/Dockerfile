FROM ubuntu:22.04@sha256:0e0a0fc6d18feda9db1590da249ac93e8d5abfea8f4c3c0c849ce512b5ef8982

RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    zlib1g-dev \
    openjdk-8-jre-headless \
    time \
    bash \
    && rm -rf /var/lib/apt/lists/*

# KMC 2.3: PanTools calls "kmc_tools sort", a command removed in KMC 3.x
RUN git clone https://github.com/refresh-bio/KMC.git /kmc
WORKDIR /kmc
RUN git checkout 0635dae65d262fe8910a46bcf03c0f77c2801442
RUN make
RUN cp bin/kmc bin/kmc_tools bin/kmc_dump /usr/local/bin/

# PanTools: use the dist/pantools.jar already present in the repository (with dist/lib)
RUN git clone https://github.com/Sheikhizadeh/pantools.git /pantools
WORKDIR /pantools
RUN git checkout 30cbd758f2e8edf7eea201438c84449a26158ffd
RUN printf '#!/bin/bash\nexec java $JAVA_OPTS -jar /pantools/dist/pantools.jar "$@"\n' > /usr/local/bin/pantools && chmod +x /usr/local/bin/pantools

RUN mkdir -p /results /input_data

CMD ["/bin/bash"]
