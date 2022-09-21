FROM spark-base
LABEL manteiner="Daniel Saad <dsaad68@gmail.com>"

# -- Layer: Image Metadata

LABEL org.label-schema.build-date=${build_date}
LABEL org.label-schema.name="Big Data Lab - JupyterLab Image"
LABEL org.label-schema.description="Spark Worker Image "
LABEL org.label-schema.url="https://github.com/dsaad89"
LABEL org.label-schema.schema-version="1.0"

# -- Runtime

EXPOSE 8081

CMD bin/spark-class org.apache.spark.deploy.worker.Worker spark://${SPARK_MASTER_HOST}:${SPARK_MASTER_PORT} >> logs/spark-worker.out