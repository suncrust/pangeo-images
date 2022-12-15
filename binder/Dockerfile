FROM pangeo/ml-notebook:latest



ENV CONDA_ENV=notebook \
    # Set username, uid and gid (same as uid) of non-root user the container will be run as
    NB_USER=jovyan \
    NB_UID=1000 \
    # Use /bin/bash as shell, not the default /bin/sh (arrow keys, etc don't work then)
    # SHELL=/bin/bash \
    # Setup locale to be UTF-8, avoiding gnarly hard to debug encoding errors
    # LANG=C.UTF-8  \
    # LC_ALL=C.UTF-8 \
    # Install conda in the same place repo2docker does
    CONDA_DIR=/srv/conda

USER root

RUN apt-get install sudo



RUN sudo apt-get pip install pypotree

RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

#RUN apt-get install cmake
#RUN mamba install pypotree
    
 # R packages including IRKernel which gets installed globally.
# r-e1071: dependency of the caret R package
RUN mamba install --quiet --yes \
    'r-base' \
    'r-caret' \
    'r-crayon' \
    'r-devtools' \
    'r-e1071' \
    'r-forecast' \
    'r-hexbin' \
    'r-htmltools' \
    'r-htmlwidgets' \
    'r-irkernel' \
    'r-nycflights13' \
    'r-randomforest' \
    'r-rcurl' \
    'r-rmarkdown' \
    'r-rodbc' \
    'r-rsqlite' \
    'r-shiny' \
    'r-tidyverse' \
    'unixodbc' && \
    #'r-lidr' && \
    mamba clean --all -f -y 
    # && \
    # fix-permissions "${CONDA_DIR}" && \
    # fix-permissions "/home/${NB_USER}"

# `rpy2` and `r-tidymodels` are not easy to install under aarch64
#  RUN set -x && \
#     arch=$(uname -m) && \
#     if [ "${arch}" == "x86_64" ]; then \
#         mamba install --quiet --yes \
#             'rpy2' \
#             'r-tidymodels' && \
#             'lidr' && \
#             mamba clean --all -f -y && \
#             fix-permissions "${CONDA_DIR}" && \
#             fix-permissions "/home/${NB_USER}"; \
#      fi;
# docker pull pangeo/ml-notebook:latest
# We recommend using a specific tag above from https://github.com/pangeo-data/pangeo-docker-images/releases
