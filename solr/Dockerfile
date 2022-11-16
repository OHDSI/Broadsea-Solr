FROM solr:8.11.1

##############################################################################
# Argument variables
##############################################################################

ARG VOCAB_VERSION
ARG VOCAB_DATABASE_SCHEMA
ARG VOCAB_JDBC_FILE_NAME
ARG VOCAB_JDBC_DRIVER_PATH
ARG VOCAB_JDBC_URL
ARG VOCAB_JDBC_USER
ARG VOCAB_JDBC_PASSWORD

##############################################################################
# Add SOLR config files
##############################################################################

WORKDIR /var/solr/data/$VOCAB_VERSION
ADD conf/ conf/
ADD core.properties .
ADD data-config.xml .

##############################################################################
# SOLR config changes
##############################################################################

USER root

# core.properties file
WORKDIR /var/solr/data/$VOCAB_VERSION
RUN sed -i "s/@vocabVersion/$VOCAB_VERSION/g" core.properties

# data-config xml file
RUN sed -i "s/@vocabDatabaseSchema/$VOCAB_DATABASE_SCHEMA/g" data-config.xml

# conf/solrconfig xml file
WORKDIR /var/solr/data/$VOCAB_VERSION/conf
RUN sed -i "s/@vocabDatabaseSchema/$VOCAB_DATABASE_SCHEMA/g" solrconfig.xml
RUN sed -i "s/@vocabJdbcDriverPath/$VOCAB_JDBC_DRIVER_PATH/g" solrconfig.xml
RUN sed -i "s/@vocabJdbcUrl/$VOCAB_JDBC_URL/g" solrconfig.xml
RUN sed -i "s/@vocabJdbcUser/$VOCAB_JDBC_USER/g" solrconfig.xml
RUN sed -i "s/@vocabJdbcPassword/$VOCAB_JDBC_PASSWORD/g" solrconfig.xml

WORKDIR /var/solr/data/$VOCAB_VERSION

RUN chown -R solr:solr /var/solr/data/$VOCAB_VERSION
USER solr
