FROM openjdk:8-slim

ARG HADOOP_VERSION=3.3.5

RUN apt-get update && apt-get install -y curl --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN curl https://archive.apache.org/dist/hadoop/core/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz \
	| tar xvz -C /opt/  \
	&& ln -s /opt/hadoop-$HADOOP_VERSION /opt/hadoop \
	&& rm -r /opt/hadoop/share/doc 

RUN ln -s /opt/hadoop/share/hadoop/tools/lib/hadoop-aws-$HADOOP_VERSION.jar /opt/hadoop/share/hadoop/common/lib/ && \
    ln -s /opt/hadoop/share/hadoop/tools/lib/aws-java-sdk-bundle-1.12.316.jar /opt/hadoop/share/hadoop/common/lib/

ENV HADOOP_HOME="/opt/hadoop"
ENV PATH="/opt/spark/bin:/opt/hadoop/bin:${PATH}"

RUN curl http://apache.uvigo.es/hive/hive-standalone-metastore-3.0.0/hive-standalone-metastore-3.0.0-bin.tar.gz \
	| tar xvz -C /opt/ \
	&& ln -s /opt/apache-hive-metastore-3.0.0-bin /opt/hive-metastore

RUN curl -L https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.47.tar.gz \
	| tar xvz -C /opt/ \
	&& ln -s /opt/mysql-connector-java-5.1.47/mysql-connector-java-5.1.47.jar /opt/hadoop/share/hadoop/common/lib/ \
	&& ln -s /opt/mysql-connector-java-5.1.47/mysql-connector-java-5.1.47.jar /opt/hive-metastore/lib/ 