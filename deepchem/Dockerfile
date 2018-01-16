FROM continuumio/miniconda3:4.3.27

# Install packages to run pycharm within the container (using singularity and a local installtion in your home)
RUN apt-get update && apt-get install -y \
    git openssh-client \
    libxtst-dev libxext-dev libxrender-dev libfreetype6-dev \
    libfontconfig1 \
    && rm -rf /var/lib/apt/lists/*

RUN groupadd -r myuser && useradd -r -g myuser myuser

WORKDIR /app

# Install requirements
COPY environment.yml /app/environment.yml

RUN conda-env create -n app -f /app/environment.yml  && rm -rf /opt/conda/pkgs/*
RUN source activate app
RUN conda install -y -q -c omnia pdbfixer=1.4 \
    && conda install -y -q -c conda-forge joblib=0.11\
    && conda install -y -q -c conda-forge six=1.10.0\
    && conda install -y -q -c deepchem mdtraj=1.9.1\
    && conda install -y -q -c conda-forge scikit-learn=0.19.1\
    && conda install -y -q -c conda-forge setuptools=36.2.2\
    && conda install -y -q -c conda-forge keras=1.2.2\
    && conda install -y -q -c conda-forge networkx=1.11\
    && conda install -y -q -c conda-forge pillow=4.3.0\
    && conda install -y -q -c conda-forge pandas=0.22.0\
    && yes | pip install tensorflow==1.4.0\
    && conda install -y -q -c conda-forge nose=1.3.7\
    && conda install -y -q -c conda-forge nose-timer=0.7.0\
    && conda install -y -q -c conda-forge flaky=3.3.0\
    && conda install -y -q -c conda-forge zlib=1.2.11\
    && conda install -y -q -c conda-forge requests=2.18.4\
    && conda install -y -q -c conda-forge xgboost=0.6a2\
    && conda install -y -q -c rdkit rdkit=2017.09.1
RUN chown -R myuser:myuser /app/*

# activate the myapp environment
ENV PATH /opt/conda/envs/app/bin:$PATH