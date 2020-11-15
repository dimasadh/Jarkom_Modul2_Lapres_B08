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

9. merubah semerub08.pw/index.php/home menjadi semerub08.pw/home

Pada UML PROBOLINGGO file /var/www/semerub08.pw, buat modul rewrite pada file .htaccess ini :
```
RewriteEngine on
RewriteCond $1 !^(index\.php|images|assets|css|js|robots\.txt|favicon\.ico)
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ ./index.php/$1 [L,QSA]
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

