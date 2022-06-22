FROM jupyter/base-notebook

USER root

EXPOSE 8050 8888

# Add virtual environment Python2.7 - Scikit-Video
RUN \
  apt-get update -y && \
  apt-get install curl software-properties-common --no-install-recommends -y && \
  add-apt-repository ppa:deadsnakes/ppa -y && \
  apt-get install python2.7 -y

RUN \
  cd / && \
  curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py && \
  python2.7 get-pip.py && \
  rm get-pip.py && \
  pip2 install virtualenv  && \
  mkdir scikitvenv && \
  chown jovyan:users -R /scikitvenv

# Copy videos, scripts, notebooks and results to image
RUN mkdir -p /home/jovyan/work/examples
COPY bycommlab.ipynb /home/jovyan/work/examples
RUN chown jovyan:users -R /home/jovyan/work/examples

USER jovyan

# Kernel for by Scikit-Video
RUN \
   python2.7 -m virtualenv /scikitvenv --system-site-packages && \
   source /scikitvenv/bin/activate && \
   pip install numpy pandas && \
   pip install ipykernel && \
   python2.7 -m ipykernel install --user --name=Scikit-Video

# Build jupyter lab
# RUN ["jupyter lab build"]

#docker run --name jupyter -it -p 8888:8888 -p 8050:8050 -e JUPYTER_ENABLE_LAB=yes jupyter
