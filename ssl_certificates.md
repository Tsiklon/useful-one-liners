# SSL Certificates
## Check expiration date on a remote site 
` # echo | openssl s_client -connect <site>:<port> 2>/dev/null | openssl x509 -noout -subject -issuer -dates `

## Validate a local Cert/CA Bundle 
` # openssl verify -CAfile /path/to/CAbundle/ /path/to/Certificate `

## Validate a Cert + Key
` # diff <(openssl  x509 -in /PATH/TO/Certificate -pubkey -noout) <(openssl rsa -in /PATH/TO/PrivateKey -pubout) `
