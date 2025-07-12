FROM docker.io/texlive/texlive:TL2016-historic AS base
RUN useradd -ms /bin/bash dev
USER dev
WORKDIR /home/dev/work/

FROM base AS dev
