FROM spark-base
LABEL manteiner="Daniel Saad <dsaad68@gmail.com>"

# -- Layer: Image Metadata

ARG build_date

LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.name="Big Data Lab - JupyterLab Image"
LABEL org.label-schema.description="Base Spark Image "
LABEL org.label-schema.url="https://github.com/dsaad89"
LABEL org.label-schema.schema-version="1.0"

# -- Runtime

EXPOSE 8080 7077

#CMD bin/spark-class org.apache.spark.deploy.master.Master >> logs/spark-master.out
CMD bin/spark-class org.apache.spark.deploy.master.Master
