FROM base
LABEL manteiner="Daniel Saad <dsaad68@gmail.com>"

# -- Layer: Image Metadata

LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.name="Big Data Lab - JupyterLab Image"
LABEL org.label-schema.description="Image for JupyterLab with Python, R and Scala kernel"
LABEL org.label-schema.url="https://github.com/dsaad89"
LABEL org.label-schema.schema-version="1.0"

# -- Layer: Notebooks

# -- Layer: JupyterLab + Python kernel for PySpark

#ARG spark_version and scala_version
ARG scala_version=2.13.1
ARG spark_version=3.3.0
ARG hadoop_version=3

# -- Layer: Python kernel 

RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential emacs-nox vim-tiny git inkscape jed \
    libsm6 libxext-dev libxrender1 lmodern netcat \
    # python dep dependencies
    python3-pip python-dev \
    # nbconvert dependencies 
    texlive-xetex texlive-fonts-recommended texlive-plain-generic \
    # ffmpeg for matplotlib anim & dvipng for latex labels
    ffmpeg dvipng \
    libhdf5-serial-dev\
    tzdata unzip nano && \
    pip3 install --upgrade pip && \
    # Clean Up
    rm -rf /var/lib/apt/lists/*

COPY . .
RUN pip3 install -r requirements.txt

# -- Layer: Scala kernel for Spark

# RUN curl -Lo coursier https://git.io/coursier-cli && \
#     chmod +x coursier && \
#     ./coursier launch --fork almond --scala ${scala_version} -- --display-name "Scala ${scala_version}" --install && \
#     # Clean Up
#     rm -f coursier

# # # # -- Layer: R kernel for SparkR

# RUN apt-get install -y r-base-dev && \
#     R -e "install.packages('IRkernel')" && \
#     R -e "IRkernel::installspec(displayname = 'R 3.5', user = FALSE)" && \
#     curl https://archive.apache.org/dist/spark/spark-${spark_version}/SparkR_${spark_version}.tar.gz -k -o sparkr.tar.gz && \
#     R CMD INSTALL sparkr.tar.gz && \
#     # Clean Up
#     rm -f sparkr.tar.gz

# -- Runtime

EXPOSE 8888
EXPOSE 4040

COPY ./workspace/ /opt/workspace/examples/

WORKDIR ${SHARED_WORKSPACE}
CMD jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root --NotebookApp.token=