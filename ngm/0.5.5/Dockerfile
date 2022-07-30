################## BASE IMAGE ######################
FROM biocontainers/biocontainers:v1.0.0_cv4

################## METADATA ######################

LABEL base_image="biocontainers:v1.0.0_cv4"
LABEL version="1"
LABEL software="NextGenMap(ngm)"
LABEL software.version="0.5.5"
LABEL about.summary="NextGenMap is a flexible highly sensitive short read mapping tool that handles much higher mismatch rates than comparable algorithms while still outperforming them in terms of runtime."
LABEL about.home="https://github.com/Cibiv/NextGenMap"
LABEL about.documentation="https://github.com/Cibiv/NextGenMap/wiki"
LABEL about.license_file="https://github.com/Cibiv/NextGenMap/blob/master/LICENSE"
LABEL about.license="MIT"
LABEL extra.identifiers.biotools="ngm"
LABEL about.tags="Genomics"
LABEL maintainer="chase mateusiak <chasem@wustl.edu>"

################## MAINTAINER ######################
MAINTAINER Saulo Alves Aflitos <sauloal@gmail.com>

################## INSTALLATION ######################

RUN conda config --add channels conda-forge && \
    conda config --add channels defaults && \
    conda config --add channels r && \
    conda config --add channels bioconda && \
    conda install nextgenmap

WORKDIR /data/
