FROM ubuntu:bionic
# ne fonctionn epas en 16.04 pb de decompression
ENV DEBIAN_FRONTEND=noninteractive
MAINTAINER Didier Debroas  <didier.debroas@uca.fr>

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

# mnimap -> https://github.com/evolbioinfo/dockerfiles/blob/master/minimap2/v2.17/Dockerfile

RUN apt-get update --fix-missing \
    && apt-get install -y wget gcc bzip2 make zlib1g zlib1g-dev \
    && cd /usr/local/ \
    && wget https://github.com/lh3/minimap2/releases/download/v2.17/minimap2-2.17.tar.bz2 \
    && tar -xjvf minimap2-2.17.tar.bz2 \
    && cd minimap2-2.17  \
    && make \
    && mv minimap2 /usr/local/bin \
    && cd .. \
    && rm -rf minimap2-2.17.tar.bz2 minimap2-2.17 \
    && apt-get remove -y wget gcc bzip2 make zlib1g-dev \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


