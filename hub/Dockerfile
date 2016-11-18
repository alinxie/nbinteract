FROM debian:jessie

RUN apt-get update
RUN apt-get install -y --no-install-recommends python3 python3-pip ca-certificates git nginx-extras lua-cjson

RUN pip3 install --upgrade pip
RUN pip3 --no-cache-dir install jupyterhub requests-futures jupyterhub-dummyauthenticator pytest webargs requests gitpython toolz
RUN jupyter nbextension install --py helpful_package

RUN pip3 --no-cache-dir install git+https://github.com/data-8/kubespawner.git@volumes
RUN pip3 --no-cache-dir install git+https://github.com/yuvipanda/jupyterhub-nginx-chp.git
RUN pip3 --no-cache-dir install git+https://github.com/data-8/nbinteract.git

RUN jupyter nbextension install --py nbinteract
RUN jupyter nbextension enable --py nbinteract

ADD jupyterhub_config.py /srv/jupyterhub_config.py

WORKDIR /srv/jupyterhub

EXPOSE 8000

CMD jupyterhub --config /srv/jupyterhub_config.py --no-ssl