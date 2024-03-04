# base image
FROM ubuntu:20.04
WORKDIR /workspace

# User setting
USER root

ARG spark_version="3.5.0"
ARG hadoop_version="3"
ARG spark_checksum="8883c67e0a138069e597f3e7d4edbbd5c3a565d50b28644aad02856a1ec1da7cb92b8f80454ca427118f69459ea326eaa073cf7b1a860c3b796f4b07c2101319"
ARG openjdk_version="11"
ARG aws_hadoop_version="3.3.4"
ARG aws_sdk_version="1.12.262"

# Ignore interactive action while building docker images
ARG DEBIAN_FRONTEND=noninteractive

ENV APACHE_SPARK_VERSION="${spark_version}" \
    HADOOP_VERSION="${hadoop_version}" \
    AWS_SDK_VERSION="${aws_sdk_version}" \
    AWS_HADOOP_VERSION="${aws_hadoop_version}"

# Install python
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    rm -rf /var/lib/apt/lists/* 
RUN apt-get update && apt-get install wget -y
RUN apt-get update && apt-get install openjdk-11-jdk -y

# Install requirements
COPY requirements.txt ./
RUN pip3 install --upgrade pip  && pip3 install --no-cache-dir -r requirements.txt
RUN apt-get clean && rm requirements.txt

# Spark installation
WORKDIR /workspace
RUN wget -q "https://archive.apache.org/dist/spark/spark-${APACHE_SPARK_VERSION}/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" && \
    echo "${spark_checksum} *spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" | sha512sum -c - && \
    tar xzf "spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" -C /workspace --owner root --group root --no-same-owner && \
    rm "spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz"

# ENV setting
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV SPARK_HOME=/workspace/spark-3.5.0-bin-hadoop3

# Configure Spark
# ENV SPARK_HOME=/opt/spark
ENV SPARK_OPTS="--driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info" \
    PATH="${PATH}:${SPARK_HOME}/bin"

# Fix Spark installation for Java 11 and Apache Arrow library
# see: https://github.com/apache/spark/pull/27356, https://spark.apache.org/docs/latest/#downloading
RUN cp -p "${SPARK_HOME}/conf/spark-defaults.conf.template" "${SPARK_HOME}/conf/spark-defaults.conf" && \
    echo 'spark.driver.extraJavaOptions -Dio.netty.tryReflectionSetAccessible=true' >> "${SPARK_HOME}/conf/spark-defaults.conf" && \
    echo 'spark.executor.extraJavaOptions -Dio.netty.tryReflectionSetAccessible=true' >> "${SPARK_HOME}/conf/spark-defaults.conf"

# Add hadoop-aws and aws-sdk
RUN wget https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/${AWS_HADOOP_VERSION}/hadoop-aws-${AWS_HADOOP_VERSION}.jar -P "${SPARK_HOME}/jars/" && \
    wget https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/${AWS_SDK_VERSION}/aws-java-sdk-bundle-${AWS_SDK_VERSION}.jar -P "${SPARK_HOME}/jars/"
# Adding JetS3t libary
RUN wget https://repo1.maven.org/maven2/net/java/dev/jets3t/jets3t/0.9.4/jets3t-0.9.4.jar -P "${SPARK_HOME}/jars/"

# Install scala kernel
RUN pip3 install jupyterlab && pip3 install spylon-kernel && python3 -m spylon_kernel install

# Jupyter workspace
WORKDIR /workspace/spark

# Expose port
EXPOSE 8888 4040

# Initial command
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]