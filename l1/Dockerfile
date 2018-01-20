FROM nvidia/cuda:8.0-cudnn6-runtime-ubuntu16.04

ARG MINICONDA_VERSION=Miniconda3-latest-Linux-x86_64

# Install miniconda
RUN apt-get update && apt-get install -y \
    wget \
    bzip2 \
    && rm -rf /var/lib/apt/lists/*
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/$MINICONDA_VERSION.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh
ENV PATH /opt/conda/bin:$PATH

# Setup environment
COPY environment.yml ./environment.yml
RUN conda env update -n root --file environment.yml

# Run
VOLUME ["/notebooks"]
WORKDIR /notebooks
EXPOSE 8888
CMD ["jupyter", "notebook", "--allow-root", "--ip=0.0.0.0"]
