# OTEL Collector multi source auth and tagging PoC

1. Generate certs:

   ```sh
   openssl req -new -sha256 -nodes -newkey rsa:4096 -keyout certs/ca.key -out certs/ca.csr
   openssl x509 -req -sha256 -extfile x509.ext -extensions ca -in certs/ca.csr -signkey certs/ca.key -days 1095 -out certs/ca.pem
   openssl req -new -sha256 -nodes -newkey rsa:4096 -keyout certs/cert.key -out certs/cert.csr
   openssl x509 -req -CA certs/ca.pem -CAkey certs/ca.key -days 730 -CAcreateserial -CAserial certs/ca.srl -extfile x509.ext -extensions v3_req -in certs/cert.csr -out certs/cert.pem
   openssl x509 -in certs/cert.pem -text -noout
   ```

1. Run `docker-compose up`
