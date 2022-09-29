FROM base
LABEL manteiner="Daniel Saad <dsaad68@gmail.com>"

# -- Layer: Image Metadata

LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.name="Spark Data Lab - Spark Base Image"
LABEL org.label-schema.description="Base Spark Image "
LABEL org.label-schema.url="https://github.com/dsaad89"
LABEL org.label-schema.schema-version="1.0"

# -- Layer: Apache Spark

#ARG spark_version and scala_version
ARG scala_version=2.13.1
ARG spark_version=3.3.0
ARG hadoop_version=3

RUN curl https://archive.apache.org/dist/spark/spark-${spark_version}/spark-${spark_version}-bin-hadoop${hadoop_version}.tgz -o spark.tgz && \
    tar -xf spark.tgz && \
    mv spark-${spark_version}-bin-hadoop${hadoop_version} /usr/bin/ && \
    echo "alias pyspark=/usr/bin/spark-${spark_version}-bin-hadoop${hadoop_version}/bin/pyspark" >> ~/.bashrc && \
    echo "alias spark-shell=/usr/bin/spark-${spark_version}-bin-hadoop${hadoop_version}/bin/spark-shell" >> ~/.bashrc && \
    echo "export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native" >> ~/.bashrc && \
    echo "export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"" >> ~/.bashrc && \
    echo "export JAVA_LIBRARY_PATH=$HADOOP_HOME/lib/native:$JAVA_LIBRARY_PATH" >> ~/.bashrc && \
    mkdir /usr/bin/spark-${spark_version}-bin-hadoop${hadoop_version}/logs && \
    rm spark.tgz

ENV SPARK_HOME /usr/bin/spark-${spark_version}-bin-hadoop${hadoop_version}
ENV SPARK_MASTER_HOST spark-master
ENV SPARK_MASTER_PORT 7077
ENV PYSPARK_PYTHON python3

# ENV PYTHONPATH=$SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.9-src.zip 
# ENV SPARK_OPTS="--driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info" 
# ENV PATH=$PATH:$SPARK_HOME/bin

# -- Runtime

WORKDIR ${SPARK_HOME}