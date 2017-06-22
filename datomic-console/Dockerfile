FROM clojure:lein-2.6.1-alpine

MAINTAINER Irina Yaroslavova Stefanova "irina.yaroslavova@ignorabilis.com"

ENV DATOMIC_VERSION 0.9.5561.50
ENV DATOMIC_HOME /opt/datomic-pro-$DATOMIC_VERSION
ARG COMPOSE_API_VERSION

# user:pass format of the file - may need a change in the future
ADD credentials.txt /tmp/credentials.txt

RUN apk add --no-cache unzip curl

RUN curl -u $(cat /tmp/credentials.txt) -SL \
     https://my.datomic.com/repo/com/datomic/datomic-pro/$DATOMIC_VERSION/datomic-pro-$DATOMIC_VERSION.zip -o /tmp/datomic.zip \
  && unzip /tmp/datomic.zip -d /opt \
  && rm -f /tmp/datomic.zip

WORKDIR $DATOMIC_HOME

# Provide a CMD with an alias to the database
# and the database uri
# e.g. CMD ["dev", "datomic:dev://db:4334/"]
ENTRYPOINT ["bin/console", "-p", "9000"]

EXPOSE 9000

CMD ["dev", "datomic:dev://datomicdb:4334"]
