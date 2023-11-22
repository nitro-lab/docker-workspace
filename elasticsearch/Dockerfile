ARG ELASTICSEARCH_VERSION
FROM elasticsearch:${ELASTICSEARCH_VERSION}

EXPOSE 9200 9300

#RUN /bin/elasticsearch-plugin install analysis-ukrainian
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-ukrainian