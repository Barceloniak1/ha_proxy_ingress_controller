# Kubernetes Ingress Certification

# First, create an SSL key and CSR (Certificate Signing Request) by running the following commands on your server:

```
mkdir -p ~/certs/YOUR_DOMAIN_NAME
cd ~/certs/YOUR_DOMAIN_NAME
(umask 077 && touch ssl.key)
openssl req -new -newkey RSA:2048 -nodes -keyout ssl.key -out ssl.csr

```

# You will be prompted to answer a few questions. There are two questions that are critical to answer correctly:

    Common name: Your domain name. For example, foo.com. Nowadays, you generally should not enter www. as 
    your Certificate Authority should make the certificate work both with www and without. However, you should 
    check with your Certificate Authority to find out.
    Password: Do not enter a password or challenge phrase. Just hit enter when you're asked for a password.

# When done, you will have a directory called certs/YOUR_DOMAIN_NAME in your home directory that contains two files:

    ssl.key—This file contains your SSL private key.
    ssl.csr—This file contains your Certificate Signing Request.

Once you have your CSR, run the following command to create a self-signed certificate:

openssl x509 -req -days 365 -in ssl.csr -signkey ssl.key -out ssl.crt

Your self-signed SSL certificate will be in the file ssl.crt.

```



STEPS IN PRACTICE:


mkdir -p ./certs/kubernetes.local
cd certs/
cd kubernetes.local/
umask 077 && touch ssl.key
openssl req -new -newkey RSA:2048 -nodes -keyout ssl.key -out ssl.csr
openssl x509 -req -days 365 -in ssl.csr -signkey ssl.key -out ssl.crt
```  
  

# K8s
```
kubectl create secret tls [jenkins] --key ssl.key --cert ssl.crt --namespace=[jenkins]
kubectl get secret [jenkins] --namespace=somenamespace -o yaml


 Copy and create secret in location of git with [jenkins], as yaml file 

*[] without brackets - example pointed out
** Make sure that domain_address in ingress has been added up to 'C:\Windows\System32\drivers\etc\hosts' Communication Computer <-> HA_Proxy (Workers) <-> Ingress <-> Service <-> Pod
```
