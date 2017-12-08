# SOLR EMBEDDED
FROM openjdk:8-jdk

RUN apt-get update && \
  apt-get install -y lsof && \
  mkdir -p /tmp/solr-5.3.1 && \
  wget http://archive.apache.org/dist/lucene/solr/5.3.1/solr-5.3.1.tgz -O /tmp/solr-5.3.1.tgz && \
  tar -xzvf /tmp/solr-5.3.1.tgz -C /tmp/solr-5.3.1 && \
  rm -rf /tmp/solr-5.3.1.tgz && \
  apt-get clean
 
