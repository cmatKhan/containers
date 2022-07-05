FROM rocker/r-ubuntu

LABEL maintainer="Chase Mateusiak <chasem@wustl.edu>"
LABEL base_image="rocker/r-ubuntu"
LABEL version="0.9.6"
LABEL software="STAARpipeline"
LABEL container="STAARpipeline"
LABEL about.summary="STAARpipeline is an R package for phenotype-genotype association analyses of WGS/WES data, including single variant analysis and variant set analysis"
LABEL about.home="https://github.com/xihaoli/STAARpipeline"
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
'BiocManager', \
'dplyr' \
),dependencies=TRUE)"
# Install STAAR dependencies from cran
RUN R -e "install.packages(c( \
'Rcpp', \
'RcppArmadillo',  \
'GMMAT', \
'Matrix', \
'kinship2' \
),dependencies=TRUE)"
# install STAAR dependencies from bioconductor
RUN R -e "BiocManager::install(c( \
'GENESIS', \
'SeqArray', \
'SeqVarTools', \
'GenomicFeatures', \
'TxDb.Hsapiens.UCSC.hg38.knownGene' \
), dependencies=TRUE)"
# install other dependencies from github
RUN R -e "remotes::install_github('xihaoli/STAAR@v0.9.6.1', dependencies=TRUE)"
RUN R -e "remotes::install_github('zilinli1988/SCANG', ref='master')"
# install STAARpipeline
RUN R -e "remotes::install_github('xihaoli/STAARpipeline',ref='main')"

USER biodocker