# Use a Debian-based devcontainer base image.
FROM mcr.microsoft.com/devcontainers/base:debian

# Install required packages including default-jdk.
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    git \
    ssl-cert \
    default-jdk \
    && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME to the apt‑installed JDK location.
ENV JAVA_HOME=/usr/lib/jvm/default-java

# Copy your Z-scaler certificate files from the project into the devcontainer.
COPY zscaler-root.pem /etc/ssl/certs/zscaler-root.pem
COPY zscaler-intermediate.pem /etc/ssl/certs/zscaler-intermediate.pem

# Concatenate intermediate and root certificate files into a single chain
# Copy chain cert to locations used by git and curl
RUN cat /etc/ssl/certs/zscaler-intermediate.pem /etc/ssl/certs/zscaler-root.pem > /etc/ssl/certs/zscaler-chain.crt && \
    mkdir -p /opt/local/share/curl && \
    mkdir -p /usr/local/share/ca-certificates && \
    cp /etc/ssl/certs/zscaler-chain.crt /opt/local/share/curl/curl-ca-bundle.crt && \
    cp /etc/ssl/certs/zscaler-chain.crt /usr/local/share/ca-certificates/curl-ca-bundle.crt && \
    update-ca-certificates

# Import the Z-scaler certificate chain into the Java keystore.
RUN keytool -importcert -noprompt -trustcacerts \
    -alias zscaler \
    -file /etc/ssl/certs/zscaler-chain.crt \
    -keystore $JAVA_HOME/lib/security/cacerts \
    -storepass changeit

# Set environment variables so that Git, curl, etc can access the updated CA bundle.
ENV SSL_CERT_FILE=/opt/local/share/curl/curl-ca-bundle.crt \
    CURL_CA_BUNDLE=/opt/local/share/curl/curl-ca-bundle.crt \
    GIT_SSL_CAINFO=/opt/local/share/curl/curl-ca-bundle.crt
