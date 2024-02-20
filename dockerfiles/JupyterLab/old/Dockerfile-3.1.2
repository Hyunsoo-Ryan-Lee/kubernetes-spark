FROM apache/spark

USER root

ARG spark_version="3.1.2"
ARG hadoop_version="3.2"
ARG spark_checksum="2385CB772F21B014CE2ABD6B8F5E815721580D6E8BC42A26D70BBCDDA8D303D886A6F12B36D40F6971B5547B70FAE62B5A96146F0421CB93D4E51491308EF5D5"
ARG openjdk_version="11"
ARG aws_hadoop_version="3.2.0"
ARG aws_sdk_version="1.11.375"

# 환경 변수 설정
ENV APACHE_SPARK_VERSION="${spark_version}" \
    HADOOP_VERSION="${hadoop_version}" \
    AWS_SDK_VERSION="${aws_sdk_version}" \
    AWS_HADOOP_VERSION="${aws_hadoop_version}"
ENV JUPYTER_ENABLE_LAB=yes

# 기본 라이브러리들 설치
RUN apt-get update --yes; \
    apt-get install --yes --no-install-recommends \
    "openjdk-${openjdk_version}-jre-headless" \
    ca-certificates-java curl awscli; \
    set -ex; \
    apt-get install -y python3 python3-pip; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*

# Spark Install
WORKDIR /opt

RUN wget -q "https://archive.apache.org/dist/spark/spark-${APACHE_SPARK_VERSION}/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" && \
    echo "${spark_checksum} *spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" | sha512sum -c - && \
    tar -zxvf "spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" -C /opt --owner root --group root --no-same-owner && \
    rm "spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz"

# Configure Spark
ENV SPARK_HOME="/opt/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}"
ENV SPARK_TGZ_URL="https://archive.apache.org/dist/spark/spark-${APACHE_SPARK_VERSION}/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz"
ENV SPARK_TGZ_ASC_URL="https://archive.apache.org/dist/spark/spark-${APACHE_SPARK_VERSION}/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz.asc"
ENV PATH="${PATH}:${SPARK_HOME}/bin"

# Fix Spark installation for Java 11 and Apache Arrow library
RUN cp -p "${SPARK_HOME}/conf/spark-defaults.conf.template" "${SPARK_HOME}/conf/spark-defaults.conf" && \
    echo 'spark.driver.extraJavaOptions -Dio.netty.tryReflectionSetAccessible=true' >> "${SPARK_HOME}/conf/spark-defaults.conf" && \
    echo 'spark.executor.extraJavaOptions -Dio.netty.tryReflectionSetAccessible=true' >> "${SPARK_HOME}/conf/spark-defaults.conf"

# Adding hadoop-aws and aws-sdk
RUN wget https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/${AWS_HADOOP_VERSION}/hadoop-aws-${AWS_HADOOP_VERSION}.jar -P "${SPARK_HOME}/jars/" && \
    wget https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/${AWS_SDK_VERSION}/aws-java-sdk-bundle-${AWS_SDK_VERSION}.jar -P "${SPARK_HOME}/jars/"
# Adding JetS3t libary
RUN wget https://repo1.maven.org/maven2/net/java/dev/jets3t/jets3t/0.9.4/jets3t-0.9.4.jar -P "${SPARK_HOME}/jars/"

# pyspark 스크립트 경로 설정
WORKDIR /workspace/pyspark

COPY . /workspace/pyspark

# 필요 라이브러리 설치 및 필요없는 디렉토리 제거
RUN pip3 install --no-cache-dir -r requirements.txt; \
    rm -rf /opt/spark