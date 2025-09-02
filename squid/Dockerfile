FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y squid apache2-utils openssl ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Create dirs
RUN mkdir -p /etc/squid/auth /etc/squid/certs /var/log/squid && \
    chown -R proxy:proxy /var/log/squid

# Copy config
COPY squid.conf /etc/squid/squid.conf

# Expose ports
EXPOSE 3128 3129

# start Squid
CMD ["sh", "-c", "chown -R proxy:proxy /var/log/squid && squid -N -d 1"]
