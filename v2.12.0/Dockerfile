# Rstudio 4.2.1 and Atlas 2.12.0 Version
FROM rocker/rstudio:4.2.1

LABEL authors="Jinwoo Yoon, Subin Kim"

RUN apt-get update && \
    apt-get install -y default-jdk

RUN R CMD javareconf
RUN R -e "install.packages('rJava', dependencies = TRUE)"

# Git Token
ARG GIT_ACCESS_TOKEN
RUN echo "GITHUB_PAT=$GIT_ACCESS_TOKEN" >> /usr/local/lib/R/etc/Renviron

# Install Devtools
RUN apt-get update
RUN apt-get install -y \
    build-essential \ 
    libcurl4-gnutls-dev \
    libxml2-dev \
    libssl-dev \
    libgit2-dev \
# Install Other
    libfontconfig1-dev \
    libcairo2-dev \
    libsodium-dev

RUN R CMD javareconf

RUN R -e "install.packages('devtools')"
RUN R -e 'install.packages("dplyr")'
RUN R -e 'install.packages("DT")'
RUN R -e 'install.packages("filelock")'
RUN R -e 'install.packages("keyring")'
RUN R -e 'install.packages("lubridate")'
RUN R -e 'install.packages("shiny")'
RUN R -e 'install.packages("renv")'

# OHDSI Packages
RUN R -e 'devtools::install_github("OHDSI/Andromeda",ref="v0.6.0")'
RUN R -e 'devtools::install_github("OHDSI/CohortGenerator",ref="v0.4.0")'
RUN R -e 'devtools::install_github("OHDSI/Cyclops",ref="v3.1.2")'
RUN R -e 'devtools::install_github("OHDSI/DatabaseConnector",ref="v5.0.2")'
RUN R -e 'devtools::install_github("OHDSI/EmpiricalCalibration",ref="v3.0.0")'
RUN R -e 'devtools::install_github("OHDSI/FeatureExtraction",ref="v3.2.0")'
RUN R -e 'devtools::install_github("OHDSI/MethodEvaluation",ref="v2.2.0")'
RUN R -e 'devtools::install_github("OHDSI/OhdsiSharing",ref="v0.2.2")'
RUN R -e 'devtools::install_github("OHDSI/ParallelLogger",ref="v3.0.0")'
RUN R -e 'devtools::install_github("OHDSI/SqlRender",ref="v1.8.3")'
RUN R -e 'devtools::install_github("OHDSI/CohortMethod",ref="v4.2.2")'

# Install JDBC driver
RUN mkdir -p /home/rstudio/temp
RUN mkdir -p /home/rstudio/jdbc
RUN mkdir -p /home/rstudio/analysis
RUN mkdir -p /home/rstudio/result
RUN R -e "DatabaseConnector::downloadJdbcDrivers(dbms = 'postgresql',pathToDriver = '/home/rstudio/jdbc')"
RUN R -e "DatabaseConnector::downloadJdbcDrivers(dbms = 'redshift',pathToDriver = '/home/rstudio/jdbc')"
RUN R -e "DatabaseConnector::downloadJdbcDrivers(dbms = 'sql server',pathToDriver = '/home/rstudio/jdbc')"
RUN R -e "DatabaseConnector::downloadJdbcDrivers(dbms = 'oracle',pathToDriver = '/home/rstudio/jdbc')"
RUN R -e "DatabaseConnector::downloadJdbcDrivers(dbms = 'spark',pathToDriver = '/home/rstudio/jdbc')"