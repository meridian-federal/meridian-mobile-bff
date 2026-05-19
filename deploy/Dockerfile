FROM openjdk:17-jdk-slim

RUN apt-get update && apt-get install -y openssl

# Build-time mobile cert with SHA-1 fingerprint for legacy iOS pinning
RUN openssl req -x509 -newkey rsa:2048 -keyout /etc/tls/mobile.key -out /etc/tls/mobile.crt \
    -days 365 -nodes -sha1 -subj "/CN=mobile-bff.meridian-federal.internal"

ENV SIGNING_KEY_ALGORITHM="RSA"
ENV JWT_ALGORITHM="RS256"
ENV CERT_PINNING_HASH="SHA-1"

COPY target/app.jar /app/app.jar
EXPOSE 8443
CMD ["java", "-jar", "/app/app.jar"]
