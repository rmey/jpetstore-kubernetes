# Build JPetStore war
FROM openjdk:8 as builder
COPY . /src
WORKDIR /src
RUN ./build.sh all

# Use WebSphere Liberty base image from the Docker Store
FROM open-liberty:20.0.0.10-kernel-java8-openj9

# Copy war from build stage and server.xml into image
COPY --from=builder /src/dist/jpetstore.war /config/apps/
COPY --from=builder /src/server.xml /config/
RUN mkdir -p /config/lib/global
COPY lib/mysql-connector-java-3.0.17-ga-bin.jar /config/lib/global
# enable postgresql Support
ADD https://jdbc.postgresql.org/download/postgresql-42.2.18.jre7.jar /config/lib/global
