## Steel Starter with Squid Proxy

### 1. Generate private key
```bash
openssl genrsa -out squid.key 2048
```

### 2. Generate self-signed certificate (valid 1 year)
```bash
openssl req -new -x509 -key squid.key -out squid.pem -days 365 \
  -subj "/C=US/ST=<State>/L=<City>/O=<Org Name>/OU=IT/CN=<your-server-ip>"
```

### 3. Build image
```bash
docker compose build
```

### 4. Create auth user "proxyuser", sometimes you have to look at the Docker image to find the name
```bash
docker run --rm -it -v $(pwd)/squid/auth:/etc/squid/auth <image-name> \
    htpasswd -c /etc/squid/auth/users proxyuser
```

### 5. Start the server
```bash
docker compose up -d
```

### 6. Accessing
  https://your-server-ip:3129 \
	•	Username: proxyuser \
	•	Password: <password provided in step 4> \
	Add in the proxy field when creating a session on Steel.dev


### **TESTING LOCALLY**
```bash
curl -x http://proxyuser:<password in step 4>@localhost:3128 https://www.google.com
```
