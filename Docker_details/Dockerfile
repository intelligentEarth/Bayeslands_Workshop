#To build this docker file
#docker build -t bayeslands .

#To run this docker build
#docker run -p 8888:8888 bayeslands

# Pull base image.
FROM badlandsmodel/pybadlands-dependencies
RUN pip install -U scikit-learn

MAINTAINER Nathaniel Butterworth

# WORKDIR /build
# RUN git clone https://github.com/badlands-model/paralleltemp_Bayeslands.git
# WORKDIR /build/paralleltemp_Bayeslands/pyBadlands/libUtils
# RUN make
# RUN pip install -e /build/paralleltemp_Bayeslands

# WORKDIR /build
# RUN git clone https://github.com/badlands-model/pyBadlands-Companion.git
# RUN pip install -e /build/pyBadlands-Companion

WORKDIR /build
RUN git clone https://github.com/badlands-model/Bayeslands_Workshop.git
WORKDIR /build/Bayeslands_Workshop/pyBadlands/libUtils
RUN make
RUN pip install -e /build/Bayeslands_Workshop

ENV TINI_VERSION v0.8.4
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/local/bin/tini
RUN chmod +x /usr/local/bin/tini

# Copy cluster configuration
#RUN mkdir /root/.ipython
#COPY profile_mpi /root/.ipython/profile_mpi

RUN mkdir /workspace 


# Copy test files to workspace
RUN cp -av /build/Bayeslands_Workshop/ /workspace
# RUN cp -av /build/pyBadlands-Companion/notebooks/* /workspace/companion/
# RUN cp -av /build/paralleltemp_Bayeslands/ptBayeslands_mountain.py /workspace/scripts

#COPY run.sh /build
#RUN chmod +x /build/run.sh

# setup space for working in
VOLUME /workspace/volume

# launch notebook
WORKDIR /workspace
EXPOSE 8888
ENTRYPOINT ["/usr/local/bin/tini", "--"]

ENV LD_LIBRARY_PATH=/workspace/Bayeslands_Workshop/pyBadlands/libUtils:/build/Bayeslands_Workshop/pyBadlands/libUtils
#CMD /build/run.sh
CMD jupyter notebook /workspace/Bayeslands_Workshop/StartHere.ipynb --ip=0.0.0.0 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.iopub_data_rate_limit=1.0e10

# To get out the profile_mpi and run.sh of this docker file, run it
# docker run -ti -v $(pwd):/workspace -p 8888:8888 badlandsmodel/pybadlands-demo-dev
# Then browse it with this
# docker exec -it 48b4fb5b215e bash