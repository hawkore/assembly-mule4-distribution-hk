# @mule.version@ and @parent.version@ is set by maven plugin. See 'https://dmp.fabric8.io/#docker:build' filtering.

FROM hawkore/openjdk:8u181

MAINTAINER hawkore

ENV HK_VERSION=@project.parent.version@
ENV VERSION=@project.parent.version@
ENV ARTIFACT=mule-standalone-hk-$VERSION.zip

# install ps, required by startup script
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -yq --no-install-recommends procps unzip

# Install mule
COPY maven/$ARTIFACT /opt/$ARTIFACT
RUN unzip /opt/$ARTIFACT -d /opt/ && rm /opt/$ARTIFACT
RUN mv /opt/mule-standalone-hk-$VERSION /opt/mule
ENV MULE_HOME /opt/mule

# Cleanup
RUN DEBIAN_FRONTEND=noninteractive apt-get purge -yq unzip && apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Define mount points.
VOLUME ["/opt/mule/logs","/opt/mule/apps","/opt/mule/domains","/opt/mule/conf","/opt/mule/work"]

# Define working directory.
WORKDIR /opt/mule

# Startup command
CMD [ "/opt/mule/bin/mule" ]

# Default http port
EXPOSE 8081
