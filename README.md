# Criar SSL para XAMPP

Passo a passo de como criar SSL para seu XAMPP no MAC ou WINDOWS

![alt text](https://raw.githubusercontent.com/alexanderbraga/ssl_macos/branch/path/to/li.png)

## Step 1: Root SSL certificate

The first step is to create a Root Secure Sockets Layer (SSL) certificate. This root certificate can then be used to sign any number of certificates you might generate for individual domains. If you aren’t familiar with the SSL ecosystem, this article from DNSimple does a good job of introducing Root SSL certificates.

Generate a RSA-2048 key and save it to a file `rootCA.key`. This file will be used as the key to generate the Root SSL certificate. You will be prompted for a pass phrase which you’ll need to enter each time you use this particular key to generate a certificate.
 
`openssl genrsa -des3 -out rootCA.key 2048`

You can use the key you generated to create a new Root SSL certificate. Save it to a file namedrootCA.pem. This certificate will have a validity of 1,024 days. Feel free to change it to any number of days you want. You’ll also be prompted for other optional information.

`openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem`


## Windows

Se você tem alguma dúvida em como configurar um certificado auto assinado em ambiente local!
Gostou compartilhe com os seus amigos =)

Scripts para instalação no diretório apache.

Primeiro vá até a pasta onde está o apache do seu Xampp, no meu caso é: 
`C:\xampp\apache`, e crie um arquivo chamado `v3.ext`, com as configurações abaixo:

`authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names`
 
`[alt_names]
DNS.1 = localhost`

Depois edite o arquivo makecert.bat que está na mesma pasta, acrescentado a seguinte linha no arquivo:

`500 -sha256 -extfile v3.ext`

Execute o makecert.bat
