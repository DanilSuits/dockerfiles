# EventStore (geteventstore.com)
#
# VERSION               0.0.2

FROM      ubuntu:14.04.2
MAINTAINER Andrew Browne <brownie@brownie.com.au>

ENV ES_VERSION 3.3.0
ENV ES_RELEASE EventStore-OSS-Ubuntu-v${ES_VERSION}
ENV ES_INSTALLER ${ES_RELEASE}.tar.gz

ADD http://download.geteventstore.com/binaries/${ES_INSTALLER} /tmp/
RUN tar xfz /tmp/${ES_INSTALLER} -C /opt && rm /tmp/${ES_INSTALLER}

EXPOSE 2113
EXPOSE 1113

VOLUME /data/db
VOLUME /data/logs

ENV EVENTSTORE_MAX_MEM_TABLE_SIZE 100000
ENV EVENTSTORE_WORKER_THREADS 12

WORKDIR /opt/${ES_RELEASE}

# TODO: There's a bug in run-node that prevents using the exec form here.  The fix appears
#       to be scheduled for the 3.4.0 release
# https://github.com/EventStore/EventStore/commit/b97b75e599e974100078074a38055851be6397e9
CMD ./run-node.sh --ext-http-prefixes=http://*:2113/ --ext-ip=0.0.0.0 \
    --db=/data/db --log=/data/logs --run-projections=all
