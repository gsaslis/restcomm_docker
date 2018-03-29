FROM openjdk:7-jre-slim

# Installs unzip
RUN apt-get update && apt-get install -y unzip

# JBoss version
ENV RESTCOMM_JAIN_SLEE_VERSION=2.9.148.102
ENV JBOSS_HOME /opt/restcomm-slee-$RESTCOMM_JAIN_SLEE_VERSION/jboss-5.1.0.GA
ENV HOME /root

# default port
EXPOSE 8080

# JAIN SLEE
ADD https://app.box.com/shared/static/vhoelesrepcbz7cblpl7a49v2jqlocfq.zip /opt/restcomm-slee-$RESTCOMM_JAIN_SLEE_VERSION.zip

RUN cd /opt && \
    unzip -qo restcomm-slee-$RESTCOMM_JAIN_SLEE_VERSION.zip && \
    rm -rf restcomm-slee-$RESTCOMM_JAIN_SLEE_VERSION.zip $JBOSS_HOME/server/all $JBOSS_HOME/server/minimal $JBOSS_HOME/docs

ENV JBOSS_DEPLOY=$JBOSS_HOME/server/default/deploy/
CMD $JBOSS_HOME/bin/run.sh -b 0.0.0.0

ARG JSS7_VERSION=7.3.1398

# Add JSS7 stack binaries 
ADD https://github.com/RestComm/jss7/releases/download/$JSS7_VERSION/restcomm-jss7-$JSS7_VERSION.zip /opt/

RUN cd /opt \
  && unzip /opt/restcomm-jss7-$JSS7_VERSION.zip


# Deploy JSS7 into JBoss (does what `ant deploy` would do)
RUN mv /opt/restcomm-jss7-$JSS7_VERSION/ss7-jboss/restcomm-ss7-service $JBOSS_DEPLOY/
RUN mv /opt/restcomm-jss7-$JSS7_VERSION/ss7/shell/bin $JBOSS_DEPLOY/bin
RUN mv /opt/restcomm-jss7-$JSS7_VERSION/ss7/shell/lib $JBOSS_DEPLOY/lib
RUN mv /opt/restcomm-jss7-$JSS7_VERSION/oam/new-ui $JBOSS_DEPLOY/

# Deploy RAs
ADD https://github.com/RestComm/jss7/releases/download/$JSS7_VERSION/RA.zip /opt/

RUN cd /opt \
  && unzip /opt/RA.zip \
  && mv /opt/RA/CAP/restcomm-slee-ra-cap-du-7.3.72.jar $JBOSS_DEPLOY/ \
  && mv /opt/RA/ISUP/restcomm-slee-ra-isup-du-7.3.72.jar $JBOSS_DEPLOY/ \
  && mv /opt/RA/MAP/restcomm-slee-ra-map-du-7.3.72.jar $JBOSS_DEPLOY/ \
  && mv /opt/RA/TCAP/restcomm-slee-ra-tcap-du-7.3.72.jar $JBOSS_DEPLOY/

# Deploy Test SBB
COPY services-DU-7.4.0-SNAPSHOT.jar $JBOSS_DEPLOY/
