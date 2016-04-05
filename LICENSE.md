FROM kaixhin/mxnet
#FROM kaixhin/cuda-mxnet:7.0

ENV REFRESHED_AT 2015-12-17
#ENV http_proxy http://10.2.133.163:808
#ENV https_proxy http://10.2.133.163:808

RUN apt-get update && apt-get install -y python-pip
RUN pip install --upgrade pip

# install ipython
# install jupyter
RUN pip install ipython jupyter

# plot figures
RUN pip install matplotlib

# dependecy package of mx.viz.plot_network
RUN pip install graphviz
# following command ensures the visualization of mx.viz.plot_network in ipython notebook
RUN apt-get install -y graphviz

#image processing
RUN pip install scipy
RUN easy_install --upgrade pip
RUN pip install -U scikit-image

# expose 8888 as jupyter's default
EXPOSE 8888

# Set a seperated workspace as working directory
WORKDIR /root/workspace
# Optionally expose the workspace to the host
VOLUME ["/root/workspace"]

# Add Tini.  Tini operates as a process subreaper for jupyter. This prevents kernel crashes.
# ADD https://github.com/krallin/tini/releases/download/v0.8.4/tini /usr/bin/tini
RUN wget -O /usr/bin/tini https://github.com/krallin/tini/releases/download/v0.8.4/tini
#RUN wget -P https://github.com/krallin/tini/releases/download/v0.8.4/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT ["/usr/bin/tini", "--"]
# Run ipython defaultly
# Run notebook for ipython defaultly
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888","--no-browser"]
