# ssl.sh
Create self signed certificate on localhost Ubuntu

## 0. Change path to yours in ssl.sh

## 1. Run SSL
`./ssl.sh local-domain.local`

## 2. Go to 
`/etc/apache2/sites-available/local-domain.local.conf` 
add:
```
<VirtualHost *:443>
	ServerAdmin webmaster@localhost
	ServerName local-domain.local
	ServerAlias local-domain.local
	DocumentRoot /var/www/local-domain.local
	<Directory />
		AllowOverride All
	</Directory>
	<Directory /var/www/local-domain.local>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride all
		Require all granted
	</Directory>
	ErrorLog /var/log/apache2/local-domain.local-error.log
	LogLevel error
	CustomLog /var/log/apache2/local-domain.local-access.log combined
	SSLEngine on
	SSLCertificateFile /home/ak/http_certs/local-domain.local/local-domain.local.crt
	SSLCertificateKeyFile /home/ak/http_certs/local-domain.local/local-domain.local.key
</VirtualHost>
```

## 3. Restart Apache and test config
`sudo service apache2 restart`

`apachectl configtest`

## 4. Add SSL to Chrome browser
https://stackoverflow.com/a/15076602/1986416
