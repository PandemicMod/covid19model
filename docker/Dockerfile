FROM rocker/tidyverse:4.0.3

RUN apt-get update
RUN apt-get install -y build-essential libxml2-dev libcurl4-openssl-dev libssl-dev

RUN apt-get install -y \
	r-cran-matrixstats r-cran-scales r-cran-gridextra \
	r-cran-bayesplot r-cran-gdata \
	r-cran-svglite r-cran-jsonlite r-cran-optparse \
	fonts-open-sans \
	fonts-arkpandora \
	fonts-adf-verana

RUN Rscript -e "update.packages(.libPaths()[1])"

RUN install2.r --error --deps FALSE \
	EnvStats BH ggplot2 isoband ggpubr nortest cowplot rstan\
	&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

WORKDIR /var/model

COPY nature nature/
COPY data data/
COPY stan-models stan-models/
COPY utils utils/
COPY *.r ./

RUN mkdir results
RUN mkdir figures
RUN mkdir web
RUN touch Rplots.pdf
RUN chmod -R a+rwx data results figures web Rplots.pdf

CMD Rscript base.r base
