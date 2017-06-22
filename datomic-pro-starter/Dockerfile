FROM clojure:lein-2.6.1-alpine

MAINTAINER Irina Yaroslavova Stefanova "irina.yaroslavova@ignorabilis.com"

ENV DATOMIC_VERSION 0.9.5561.50
ENV DATOMIC_HOME /opt/datomic-pro-$DATOMIC_VERSION
ENV DATOMIC_DATA $DATOMIC_HOME/data

RUN apk add --no-cache unzip curl

# user:pass format of the file - may need a change in the future
ADD credentials.txt /tmp/credentials.txt
RUN echo $(cat /tmp/credentials.txt)

RUN curl -u $(cat /tmp/credentials.txt) -SL \
     https://my.datomic.com/repo/com/datomic/datomic-pro/$DATOMIC_VERSION/datomic-pro-$DATOMIC_VERSION.zip -o /tmp/datomic.zip \
  && unzip /tmp/datomic.zip -d /opt \
  && rm -f /tmp/datomic.zip

ADD config $DATOMIC_HOME/config

WORKDIR $DATOMIC_HOME
RUN echo DATOMIC HOME: $DATOMIC_HOME
ENTRYPOINT ["./bin/transactor"]

# Provide a CMD argument with the relative path to the
# transactor.properties file it will supplement the ENTRYPOINT
VOLUME $DATOMIC_DATA

EXPOSE 4334 4335 4336

CMD ["config/dev-transactor.properties"]

ADD restore-db.sh /usr/local/bin/restore-db
