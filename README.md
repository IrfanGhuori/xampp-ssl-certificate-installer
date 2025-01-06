

[![Behance](https://img.shields.io/badge/Behance-1769ff?logo=behance&logoColor=white)](https://behance.net/Irfan_Ghuori) [![Facebook](https://img.shields.io/badge/Facebook-%231877F2.svg?logo=Facebook&logoColor=white)](https://facebook.com/irfan.whitehead) [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/irfan-ghuori-39b410155/) [![Pinterest](https://img.shields.io/badge/Pinterest-%23E60023.svg?logo=Pinterest&logoColor=white)](https://pinterest.com/irfanghuori_) 

# 💻 Tech Stack:
![PHP](https://img.shields.io/badge/php-%23777BB4.svg?style=for-the-badge&logo=php&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white) ![Apache Groovy](https://img.shields.io/badge/Apache%20Groovy-4298B8.svg?style=for-the-badge&logo=Apache+Groovy&logoColor=white) ![AssemblyScript](https://img.shields.io/badge/assembly%20script-%23000000.svg?style=for-the-badge&logo=assemblyscript&logoColor=white) ![Nodemon](https://img.shields.io/badge/NODEMON-%23323330.svg?style=for-the-badge&logo=nodemon&logoColor=%BBDEAD) ![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi) ![Xamarin](https://img.shields.io/badge/Xamarin-3199DC?style=for-the-badge&logo=xamarin&logoColor=white) ![Apache](https://img.shields.io/badge/apache-%23D42029.svg?style=for-the-badge&logo=apache&logoColor=white) ![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=Apache%20Airflow&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white) ![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white) ![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white) ![Sequelize](https://img.shields.io/badge/Sequelize-52B0E7?style=for-the-badge&logo=Sequelize&logoColor=white) ![Adobe](https://img.shields.io/badge/adobe-%23FF0000.svg?style=for-the-badge&logo=adobe&logoColor=white) ![Adobe Illustrator](https://img.shields.io/badge/adobe%20illustrator-%23FF9A00.svg?style=for-the-badge&logo=adobe%20illustrator&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white) ![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)



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

