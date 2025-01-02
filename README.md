# How to Create Valid SSL in localhost for XAMPP
## _The Last Markdown Editor, Ever_

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)



Chrome browser updates has become a burden for local development. Not only they decided to disable .dev domain for local development, they also really have specific configuration in SSL Cert to show the site as secure.

In this step by step tutorial I will try to explain  the walk-through to create SSL cert locally to be used in XAMPP in Windows.

In my XAMPP install I basically  have a clone to all the site that I managed.  And All of them (of course) use SSL/HTTPS.

![alt text](https://i.ibb.co/5xK8V4P/xampp-local-ssl-screenshot.png)

Here’s the step by  step guide:
In this step we are going to crate SSL and setup “site.test” website.

## 1. Navigate to Apache directory in XAMPP.

In regular install it’s in C:\xampp\apache.

## 2. Create a folder in that page.
This is where we will store our cert. In this example I will create “crt” folder. So we will have C:\xampp\apache\crt

## 3. Add this files Download from repository.

cert.conf
make-cert.bat

## 4. Edit cert.conf and Run make-cert.bat
Change {{DOMAIN}} text using the domain we want to use, in this case site.test and save.

Double click the make-cert.bat and input the domain site.test when prompted. And just do enter in other question since we already set the default from cert.conf.

![alt text](https://i.ibb.co/H72JTj3/make-cert.png)

## 5. Install the cert in windows.
After that, you will see site.test folder created. In that folder we will have server.crt and server.key. This is our SSL certificate.

Double click on the server.crt to install it on Windows so Windows can trust it.
![alt text](https://i.ibb.co/NjCrxLd/cert-window.png)

And then select Local Machine as Store Location.

![alt text](https://i.ibb.co/zS5Lhyx/install-cert.png)

And then Select “Place all certificate in the following store” and click browse and select Trusted Root Certification Authorities.

![alt text](https://i.ibb.co/9HHJ7LG/install-cert-as-trusted.png)
Click Next and Finish.

And now this cert is installed and trusted in Windows. Next is how how to use this cert in XAMPP.

## 6. Add the site in Windows hosts
1- Open notepad as administrator.
2- Edit C:\Windows\System32\drivers\etc\hosts (the file have no ext)
3- Add this in a new line:
```sh
127.0.0.1 site.test
```
This will tell windows to load XAMPP when we visit http://site.test You can try and it will show XAMPP dashboard page.

## 7. Add the site in XAMPP conf.
We need to enable SSL for this domain and let XAMPP know where we store the SSL Cert. So we need to edit C:\xampp\apache\conf\extra\httpd-xampp.conf
And add this code at the bottom:
```sh
## site.test
 <VirtualHost *:80>
     DocumentRoot "C:/xampp/htdocs"
     ServerName site.test
     ServerAlias *.site.test
 </VirtualHost>
 <VirtualHost *:443>
     DocumentRoot "C:/xampp/htdocs"
     ServerName site.test
     ServerAlias *.site.test
     SSLEngine on
     SSLCertificateFile "crt/site.test/server.crt"
     SSLCertificateKeyFile "crt/site.test/server.key"
 </VirtualHost>
```

After that, you will need to restart Apache in XAMPP.  It’s very simple, simply open XAMPP Control Panel and Stop and re-Start Apache Module.

## 8. Restart your browser and Done!
This is required to load the certificate. And visit the domain on your browser, and you will see green lock!

```sh
127.0.0.1:8000
```

## License

MIT

