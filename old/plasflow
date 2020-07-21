FROM ubuntu:bionic
ENV DEBIAN_FRONTEND=noninteractive
MAINTAINER Christian Brandt <christian.jena@gmail.com

RUN apt-get update && apt-get install -y --no-install-recommends \
					 wget
RUN apt-get clean

# install correct conda version for plasflow
RUN wget --no-check-certificate https://repo.continuum.io/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh
RUN bash Miniconda3-4.5.11-Linux-x86_64.sh -b -p /conda
RUN rm -f Miniconda3-4.5.11-Linux-x86_64.sh

ENV PATH /conda/bin:$PATH
# install plasflow
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda install plasflow -c smaegol
RUN conda install -c bioconda perl-bioperl perl-getopt-long
# modify shebangs for bioperl
RUN sed -i '1i#!/conda/bin/perl' /conda/bin/filter_sequences_by_length.pl
