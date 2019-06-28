# vscode-liveserver-https
How to enable HTTPS protocol on live server Visual Code

First you will need a self-signed SSL Certificate. If you don’t know how to create a self-signed SSL Certificate goto https://www.akadia.com/services/ssh_test_certificate.html and follow the steps.

If you are using Visual Code in windows, check if you have Git for Windows, which comes with OpenSSL in "C:\Program Files\Git\mingw64\bin\openssl.exe", if not download OpenSSL from a mirror of your choice https://wiki.openssl.org/index.php/Binaries

Open Command Prompt
cd D:\https\
D:
"C:\Program Files\Git\mingw64\bin\openssl.exe" req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout mycert.pem -out mycert.pem
<fill in your details>
"C:\Program Files\Git\mingw64\bin\openssl.exe" pkcs12 -export -out mycert.pfx -in mycert.pem -name "My Certificate"
<fill in password, e.g.12345>
 
REM create a file containing key and self-signed certificate
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout mycert.pem -out mycert.pem
REM export mycert.pem as PKCS#12 file, mycert.pfx
openssl pkcs12 -export -out mycert.pfx -in mycert.pem -name "My Certificate"


After you have the private key and certificate:

- Go to your visual code project.
- Create ```.vscode``` folder inside the project. ( Don’t forget the . (period) ).
- Inside that folder create ```settings.json``` file.
- Paste the following code:

  ```json
  {  
  "liveServer.settings.https":   
  {
  "enable": true, //set it true to enable the feature.  
  "cert": "D:\\https\\mycert.pfx", //full path of the certificate  
  "key": "D:\\https\\mycert.pem", //full path of the private key  
  "passphrase": "12345"  
  }  
  }
  ```
  
- Start the Live Server and access your project using HTTPS
