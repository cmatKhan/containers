FROM rocker/r-ubuntu

LABEL maintainer="Chase Mateusiak <chasem@wustl.edu>"
LABEL base_image="rocker/r-ubuntu"
LABEL version="0.9.6.1"
LABEL software="STAAR"
LABEL container="STAAR"
LABEL about.summary="STAAR is an R package for performing variant-Set Test for Association using Annotation infoRmation (STAAR) procedure in whole-genome sequencing (WGS) studies"
LABEL about.home="https://github.com/xihaoli/STAAR"
LABEL about.license="GPL-3"
LABEL about.tags="field::biology, field::biology:bioinformatics"

USER root

RUN echo "options(repos = c(CRAN = 'https://cran.rstudio.com/'), download.file.method = 'libcurl')" >> /usr/lib/R/etc/Rprofile.site

# Add a directory for host R libraries
RUN mkdir -p /library
RUN echo "R_LIBS_SITE=/library:\${R_LIBS_SITE}" >> /usr/lib/R/etc/Renviron.site

# Download openblas
RUN  apt-get update
RUN  apt-get install -y --no-install-recommends \
    software-properties-common \
    dirmngr \
    wget \
    libopenblas-base
# Clean up
RUN apt-get autoremove -y && autoclean -y

# Set BLAS and LAPACK to openblas
RUN update-alternatives --set libblas.so.3-x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/openblas-pthread/libblas.so.3
RUN update-alternatives --set liblapack.so.3-x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/openblas-pthread/liblapack.so.3

# Install easy R-packages
RUN R -e "install.packages(c( \
'remotes', \
'BiocManager' \
),dependencies=TRUE)"
# Install STAAR dependencies from cran
RUN R -e "install.packages(c( \
'Rcpp', \
'RcppArmadillo',  \
'GMMAT', \
'Matrix' \
),dependencies=TRUE)"
# install STAAR dependencies from bioconductor
RUN R -e "BiocManager::install('GENESIS', dependencies=TRUE)" 
# install STAAR
RUN R -e "remotes::install_github('xihaoli/STAAR', dependencies=TRUE)"

USER biodocker