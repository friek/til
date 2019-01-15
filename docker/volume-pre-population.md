# Docker volume pre-population
When building a docker container, it is possible to pre-populate exposed volumes 
with data. To achieve this, the order of commands in Dockerfile important.

I previously thought that the VOLUME command should come before adding any files. 
This turned out to be wrong. This is an example of a working configuration

```dockerfile
FROM jboss/wildfly

# Set up the configuration, data and log directories.
USER root
RUN mkdir -p /opt/jboss/wildfly/{domain,standalone}/configuration /opt/jboss/wildfly/standalone/{log,data} && \
	chown jboss /opt/jboss/wildfly/{domain,standalone}/configuration /opt/jboss/wildfly/standalone/{log,data}
USER jboss

# Copy the configuration
ADD --chown=jboss configs/ /opt/jboss/wildfly/standalone/configuration/

VOLUME ["/opt/jboss/wildfly/standalone/log", "/opt/jboss/wildfly/standalone/data"]
```

When a new container is started with fresh volumes, docker will populate them 
the way they were created in the container.
