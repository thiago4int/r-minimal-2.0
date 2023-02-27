# Step 1: Build the R lang environment
FROM rocker/r-ver:4.0.4 AS r-base

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libxml2-dev \
    libssl-dev \
    libcurl4-openssl-dev \
    libgit2-dev \
    libpq-dev \
    libudunits2-dev \
    libgdal-dev \
    libgeos-dev

# Install R packages required by the R package, including specific versions
RUN install2.r --error \
    remotes \
    && Rscript -e "remotes::install_version('dplyr', '1.0.7')" \
    && Rscript -e "remotes::install_version('ggplot2', '3.3.5')" \
    && Rscript -e "remotes::install_version('lubridate', '1.7.10')" \
    && Rscript -e "remotes::install_version('sf', '1.0-2')" \
    && Rscript -e "remotes::install_version('tidyr', '1.1.4')" \
    && Rscript -e "remotes::install_version('magrittr', '2.0.1')" \
    && Rscript -e "remotes::install_version('readr', '2.1.1')" \
    && Rscript -e "remotes::install_version('leaflet', '2.0.3')"

# Step 2: Add an R package and safely remove its unnecessary dependencies
FROM r-base AS add-package

RUN install2.r --error \
    my-r-package \
    && Rscript -e "remotes::prune_installed()"

# Step 3: Copy the installed R packages to a smaller Alpine image
FROM alpine:3.14

RUN apk add --no-cache bash

COPY --from=add-package /usr/local/lib/R/site-library /usr/local/lib/R/site-library

CMD ["R"]