FROM ubuntu:22.04@sha256:0e0a0fc6d18feda9db1590da249ac93e8d5abfea8f4c3c0c849ce512b5ef8982

RUN apt-get update && apt-get install -y \
    ca-certificates \
    wget \
    unzip \
    time \
    bash \
    && rm -rf /var/lib/apt/lists/*

# Precompiled binaries of release v0.5.1 (bioconda release build), verified with SHA-256
RUN wget -q https://github.com/GeneDx/pgr-tk/releases/download/v0.5.1/pgr-tk-v0.5.1.zip -O /tmp/pgr-tk.zip \
    && echo "f7252d6ef3640f28ca8c88cb9e469fad63799e467272dcdba24fa40026635864  /tmp/pgr-tk.zip" | sha256sum -c - \
    && unzip -q /tmp/pgr-tk.zip -d /pgr-tk \
    && rm /tmp/pgr-tk.zip
RUN cp /pgr-tk/release/pgr-* /usr/local/bin/ && chmod +x /usr/local/bin/pgr-*

RUN mkdir -p /results /input_data

CMD ["/bin/bash"]
