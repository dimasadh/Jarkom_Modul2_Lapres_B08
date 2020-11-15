# Lapres Modul 2 Jarkom - Kelompok B08

Dimas Adhitya 05111840000015

Salim Bin Usman 05111840000104


1. alamat semerub08.pw

*Pada UML MALANG file  /etc/bind/named.conf.local, isikan
```
zone "jarkom2020.com" {
	type master;
	file "/etc/bind/jarkom/jarkom2020.com";
};
```

*Pada UML MALANG file /etc/bind/jarkom/semerub08.pw, tambahkan
```
@	IN	NS	semerub08.pw.
@	IN	A	10.151.83.76	;IP PROBOLINGGO
```

2. alias www.semerub08.pw

*Pada UML MALANG file /etc/bind/jarkom/semerub08.pw, tambahkan
```
www	IN	CNAME	semerub08.pw.
```

3. subdomain penanjakan.semerub08.pw

*Pada UML MALANG file /etc/bind/jarkom/semerub08.pw, tambahkan
```
penanjakan	IN	A	10.151.83.76	;IP PROBOLINGGO
```

4. reverse domain pada semerub08.pw

*Pada UML MALANG file /etc/bind/named.conf.local, tambahkan
```
zone "83.151.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/83.151.10.in-addr.arpa";
};
```

*Pada UML MALANG file /etc/bind/jarkom/83.151.10.in-addr.arpa, tambahkan
```
83.151.10.in-addr.arpa	IN	NS	semerub08.pw.
76				IN	PTR	semerub08.pw.	;BYTE KE-4 PROBOLINGGO
```

5. dns slave domain semerub08.pw pada MOJOKERTO

*Pada UML MALANG file /etc/bind/named.conf.local, tambahkan
```
zone "semerub08.pw" {
    type master;
    notify yes;
    also-notify { 10.151.83.75; };
    allow-transfer { 10.151.83.75; };
    file "/etc/bind/jarkom/semerub08.pw";
};
```

*Pada UML MOJOKERTO file /etc/bind/named.conf.local, tambahkan
```
zone "semerub08.pw" {
    type slave;
    masters { 10.151.83.74; };
    file "/var/lib/bind/semerub08.pw";
};
```

6. subdomain gunung.semerub08.pw yang didelegasikan pada MOJOKERTO

*Pada UML MALANG file /etc/bind/jarkom/semerub08.pw, tambahkan
```
ns1	IN	A	10.151.83.75	;IP MOJOKERTO
gunung	IN	NS	ns1
```

*Pada UML MALANG file /etc/bind/named.conf.options, tambahkan
```
allow-query{any;};
```

*Pada UML MALANG file /etc/bind/named.conf.local, tambahkan
```
zone "semerub08.pw" {
    type master;
    notify yes;
    also-notify { 10.151.83.75; };
    allow-transfer { 10.151.83.75; };
    file "/etc/bind/jarkom/semerub08.pw";
};
```

*Pada UML MOJOKERTO file /etc/bind/named.conf.options, tambahkan
```
allow-query{any;};
```

*Pada UML MOJOKERTO file /etc/bind/named.conf.local, tambahkan
```
zone "gunung.semerub08.pw" {
    type master;
    file "/etc/bind/delegasi/gunung.semerub08.pw";
    allow-transfer { any; };
};
```

*Pada UML MOJOKERTO file /etc/bind/delegasi/gunung.semerub08.pw, tambahkan
```
@	IN	NS	gunung.semerub08.pw
@	IN	A	10.151.83.76		;IP PROBOLINGGO
```

7. subdomain naik.gunung.semerub08.pw

	*Pada UML MOJOKERTO file /etc/bind/delegasi/gunung.semerub08.pw, tambahkan
  ```
	@	IN	NS	gunung.semerub08.pw
  @	IN	A	10.151.83.76		;IP PROBOLINGGO
  naik	IN	A	10.151.83.76		;IP PROBOLINGGO
  ```

8. Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw.
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/semerub08.pw, menambahkan 
```
ServerName semerub08.pw
ServerAlias www.semerub08.pw
DocumentRoot /var/www/semerub08.pw
```

*Pada UML PROBOLINGGO directory /var/www/semerub08.pw mengisi dengan file yang telah disediakan
![image](https://user-images.githubusercontent.com/55347970/99186132-c2a7b500-2780-11eb-97e7-40a4c5fa83ba.png)


9. merubah semerub08.pw/index.php/home menjadi semerub08.pw/home

*Pada UML PROBOLINGGO file /var/www/semerub08.pw, buat modul rewrite pada file .htaccess ini :
```
RewriteEngine on
RewriteCond $1 !^(index\.php|images|assets|css|js|robots\.txt|favicon\.ico)
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ ./index.php/$1 [L,QSA]
```
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/semerub08.pw, menambahkan
```
<Directory /var/www/semerub08.pw>
	Options +FollowSymLinks -Multiviews
	AllowOverride All
</Directory>
```

10. Web http://penanjakan.semerub08.pw memiliki DocumentRoot /var/www/penanjakan.semerub08.pw
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/penanjakan.semerub08.pw, menambahkan 
```
ServerName penanjakan.semerub08.pw
DocumentRoot /var/www/penanjakan.semerub08.pw
```
*Pada UML PROBOLINGGO directory /var/www/penanjakan.semerub08.pw mengisi dengan file yang telah disediakan
![image](https://user-images.githubusercontent.com/55347970/99186341-3e563180-2782-11eb-888c-e5c7bc966e03.png)

11. Allow Directory listing /public dan Denied untuk directory didalamnya
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/penanjakan.semerub08.pw, menambahkan
```
<Directory /var/www/penanjakan.semerub08.pw/public>
	Options +Indexes
</Directory>
<Directory /var/www/penanjakan.semerub08.pw/public/javascripts>
	Options -Indexes
</Directory>
<Directory /var/www/penanjakan.semerub08.pw/public/css>
	Options -Indexes
</Directory>
<Directory /var/www/penanjakan.semerub08.pw/public/images>
	Options -Indexes
</Directory>
```

12. Mengubah tampilan page HTTP Error code 404 dengan file /errors/404.html
*Pada UML PROBOLINGGO file /var/www/penanjakan.semerub08.pw/.htaccess
```
ErrorDocument 404 /errors/404.html
```
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/penanjakan.semerub08.pw, menambahkan
```
<Directory /var/www/penanjakan.semerub08.pw>
	Options +FollowSymLinks -Multiviews
	AllowOverride All
</Directory>
```

13. Alias dari http://penanjakan.semerub08.pw/public/javascripts menjadi http://penanjakan.semerub08.pw/js
* Pada UML PROBOLINGGO file /etc/apache2/sites-available/penanjakan.semerub08.pw, menambahkan
```
Alias "/js" "/var/www/penanjakan.semerub08.pw/public/javascripts"
```

14. Web http://naik.gunung.semerub08.pw dengan port 8888
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/naik.gunung.semerub08.pw, menambahkan 
```
<VirtualHost *:80> -> *:8888
	ServerName naik.gunung.semerub08.pw
	DocumentRoot /var/www/naik.gunung.semerub08.pw
```
*Pada UML PROBOLINGGO file /etc/apache2/ports.conf, menambahkan
```
Listen 8888
```

*Pada UML PROBOLINGGO directory /var/www/semerub08.pw mengisi dengan file yang telah disediakan

15. Autentikasi password web http://naik.gunung.semerub08.pw dengan username "semeru" dan password "kuynaikgunung"
*Pada UML PROBOLINGGO file /var/www/.htpasswd, menambahkan username dan password yang telah dienkripsi
```
semeru:$apr1$v86fp5n4$ZqyQF.daJu7bxryFF6zJ81
```

*Pada UML PROBOLINGGO file /var/www/naik.gunung.semerub08.pw/.htaccess, menambahkan
```
AuthType Basic
AuthName "Private Content!"
AuthUserFile /var/www/.htpasswd
Require valid-user
```

16. Redirect pengaksesan IP probolinggo menuju web http://semerub08.pw
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/default, menambahkan
```
DocumentRoot /var/www/semerub08.pw
```

17. Redirect semua request dari /var/www/penanjakan.semerub08.pw/public/images yang memiliki substring semeru menuju gambar semeru.jpg
*Pada UML PROBOLINGGO file /var/www/penanjakan.semerub08.pw/.htaccess, menambahkan
```
RewriteEngine On
RewriteCond %{REQUEST_URI} !/public/images/semeru.jpg
RewriteRule ^(.*)semeru(.*)$ /public/images/semeru.jpg [R,L]
```
*Pada UML PROBOLINGGO file /etc/apache2/sites-available/penanjakan.semerub08.pw, menambahkan
```
<Directory /var/www/penanjakan.semerub08.pw>
	Options +FollowSymLinks -Multiviews
	AllowOverride All
</Directory>
```


note :
`mengacu pada referensi gambar`

Referensi Gambar :

MALANG

![alt text](https://lh4.googleusercontent.com/Rb0mT-y8r73eba0uWuXo5bROHLVUxIIKpZCpUQ_RO84fIynnHEhZFaDLrGRRB8GEOZt7j7pyw1wPJOjDZTSW9Mls2qFnhk3UCllxRgR0GMNpZyBL6MIQUYs9wpHw6zvV99C6bn4g)


![alt text](https://lh4.googleusercontent.com/r723LWJ_bIUDtQSzryiiw52kqNwXwxlnBn4VqMv7amO85rM6OWc7n0EKAXVe_IvClgS8uuVX2H43_JlFbSBcC0xgaez-vTZeEKsV1l8)


![alt text](https://lh6.googleusercontent.com/Q0uCOeB4NKYTvxhuz8l37zKLHDNcI8CwFsny7uOKqAM8GJoVGxQX-ZldbYeTBFCanrX5OqikvkNxKbzsjdjnPy2bGedBr_s24HP2hRw)


![alt text](https://lh6.googleusercontent.com/sUXacRED1eMuwnwfa01WQWNHW41O59TaHqofdEDEusOqx6Gb35YPDrKSytRxiIIoiXdraNaoYxdY1XlrSXs55ezb7oFcU0I1XbaRN057SbVNYRWwKnC3ioLmCxR_pehko3Tm7Cab)


MOJOKERTO

![alt text](https://lh6.googleusercontent.com/WXkU6XyIvNj6tN3Rlw31RqIAkyx2GFBlitdVUhOuvzji7T6ezwGVgPqRDM-FVYx9iPLFDU-umjJ1WPHCrDVF-NyPW3HfPFYnYqJlGBY)


![alt text](https://lh4.googleusercontent.com/c_7hre6RGpImQddcQWLYvGxmHcvwuZvv9E9-2aQpIa1fkM5uFybucS0Cda-cO63fKuvJtMDhYc4vGJ_QVo_GeGkpDFxC2w_9l6VTvps)


![alt text](https://lh6.googleusercontent.com/0hMW361tT_NTH68xwMNyhUbCuk7kM1APVhUvrieKMMac215aBd2sebDLyf_wyK0sAETyeUOl02JN6CnwiM0qM1kJV9cmXXFF0OjOBNo)
