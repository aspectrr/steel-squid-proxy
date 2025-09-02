FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y squid apache2-utils openssl && \
    rm -rf /var/lib/apt/lists/*

# Create dirs
RUN mkdir -p /etc/squid/auth /etc/squid/certs

# Copy config
COPY squid.conf /etc/squid/squid.conf

EXPOSE 3129

CMD ["squid", "-N", "-d", "1"]
