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


![alt text](https://lh6.googleusercontent.com/Y4LJ7uruycE4l_2Xl2K5OFkGIyA-_NuJ8cUkH0wmyWcekB3ogq54MklVK6RJuzO6-CARJRro6sMZ3Vc9nodpkhV0mpXqnDGBSmIyNow)


![alt text](https://lh5.googleusercontent.com/fzAW6t2Oq_45PUKa00OsztcpuoJZ8RzlorTyY2AzkepPulVBjGxqfy1Ht1KStlraCfYF1RmPpMBXDRjmF5Na-okkKDeE6dhIuAi0vn0)


![alt text](https://lh6.googleusercontent.com/sUXacRED1eMuwnwfa01WQWNHW41O59TaHqofdEDEusOqx6Gb35YPDrKSytRxiIIoiXdraNaoYxdY1XlrSXs55ezb7oFcU0I1XbaRN057SbVNYRWwKnC3ioLmCxR_pehko3Tm7Cab)


MOJOKERTO

![alt text](https://lh4.googleusercontent.com/4VcrDIeresl6FsZQ2aka-ntG0uMR6YDJo-2s9TGW841JUg7dr6blk7POPpJ-hl-Hw4kH_SYc1R3UYNC0NzVYbmi-te4phLmooXli_FQ)


![alt text](https://lh6.googleusercontent.com/25a0bUOz7YijQL35m5ifbfiqWTql7gFyyT1rlYGTaGxUi61a-jwV2ZZwxvllIvYYmooVtL9RX75JqAbfYjvtE3w_ixbVpgFt68Zow7g)


![alt text](https://lh6.googleusercontent.com/Rt8blgOwMBzz_mbDb4dFDG1aUNwO_nMsorgbYN4EUJdwWIovpkhgBBIlUeEYufMpBztF6P49kEv7NJ2GDcFLdzQRyk3G1CbYPjujIi8)

