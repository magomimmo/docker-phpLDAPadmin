# osixia/phpldapadmin

A docker image to run phpLDAPadmin.
> [phpldapadmin.sourceforge.net](http://phpldapadmin.sourceforge.net)


## Quick start

Run a phpLDAPadmin docker image by replacing `ldap.example.com` with your ldap host or IP :

    sudo docker run -p 443:443 \
               -e LDAP_HOSTS=ldap.example.com \
               -d osixia/phpldapadmin

That's it :) you can access phpLDAPadmin on **https://localhost**


## Examples

### OpenLDAP & phpLDAPadmin in 1''

### HTTPS

#### Use autogenerated certificate
By default HTTPS is enable, a certificate is created for the CN (common name) example.org. To work properly on your server adjust SERVER_NAME environment variable to match the phpLDAPadmin server CN.

	docker run -e SERVER_NAME=phpldapadmin.my-compagny.com -d osixia/phpldapadmin

#### Use your own certificate

Add your custom certificate, private key and CA certificate in the directory **image/service/phpldapadmin/assets/apache2/ssl** adjust filename in **image/env.yml** and rebuild the image ([see manual build](#manual-build)).

Or you can set your custom certificate at run time, by mouting your a directory containing thoses files to **/osixia/phpldapadmin/apache2/ssl** and adjust there name with the following environment variables :

	docker run -v /path/to/certifates:/osixia/phpldapadmin/apache2/ssl \
	-e SSL_CRT_FILENAME=my-phpldapadmin.crt \
	-e SSL_KEY_FILENAME=my-phpldapadmin.key \
	-e SSL_CA_CRT_FILENAME=the-ca.crt \
	-d osixia/phpldapadmin

Ommit the -e SSL_CA_CRT_FILENAME variable for self signed certificates

#### Disable HTTPS
Add -e HTTPS=false to the run command :

    docker run -e HTTPS=false -d osixia/phpldapadmin

## Environment Variables

## Manual build

Clone this project :

	git clone https://github.com/osixia/docker-phpLDAPadmin
	cd docker-mariadb

Adapt Makefile, set your image NAME and VERSION, for example :

	NAME = osixia/phpldapadmin
	VERSION = 0.5.0
	
	becomes :
	NAME = billy-the-king/phpldapadmin
	VERSION = 0.1.0

Build your image :
	
	make build
	
Run your image :

	docker run -d billy-the-king/phpldapadmin:0.1.0

## Tests

We use **Bats** (Bash Automated Testing System) to test this image:

> [https://github.com/sstephenson/bats](https://github.com/sstephenson/bats)

Install Bats, and in this project directory run :

	make test

	

