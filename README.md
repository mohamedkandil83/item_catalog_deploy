# item_catalog_deploy

## task2:
* IP Add `13.232.58.110`
* SSH Port `2200`
* URL `13.232.58.110.xip.io`
### Summary"
First, you'll need to run:
* `sudo apt-get install apache2 mysql-client mysql-server`

* Once you do that, you'll get the start up page for MySQL, where you will need to set your root user for MySQL. This is the specific MySQL root user, not your server root user.
That setup should take about 20-30 seconds. After that, we need to get WSGI, so run the following:
`sudo apt-get install libapache2-mod-wsgi`

* Once we have that, we need to make sure we've enabled WSGI with the following:
`sudo a2enmod wsgi`

* It is probably already enabled from the installation, but it is a good idea to make sure.
Next we are ready to set up our Flask environment.
Run:
`cd /var/www/`

* Now let's make our Flask environment directory:
`mkdir FlaskApp`

* Move into that directory:
`cd FlaskApp`

* Now make the actual application directory:
`mkdir FlaskApp`

* Now let's go in there:
`cd FlaskApp/`

* Now we're going to make two directories, static and template:
  - `mkdir static`
  - `mkdir templates`

* Now we're ready to create the main file for your first Flask App:
`nano __init__.py`


* Here is where we have our initialization script for our Flask application. You can actually keep all of your main website code right here for simplicity's sake, and that's what we'll be doing. Within your init.py file, you will type:
```
#! /bin/usr/python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def homepage():
    return "Hello From Flask"


if __name__ == "__main__":
    app.run()

==========================================
```

* To get Flask, we're going to use pip, so you will need to first get pip if you do not already have it:
`apt-get install python-pip`

* Now that we have pip, we also need virtualenv to create the virtual environment for Flask to run Python and your application in:
`pip install virtualenv`

* Now to set up the virtualenv directory:
`sudo virtualenv venv`

* Activate the virtual environment:
`source venv/bin/activate`

* Now install Flask within your virtual environment:

`pip install Flask`

* Find out if everything worked out by going:
`python init.py`

==========================

* So now we need to set up our Flask configuration file:
`vi /etc/apache2/sites-available/FlaskApp.conf`

* This is where your Flask configuration goes, which will apply to your live web site. Here's the code that you need to include:
```
<VirtualHost *:80
                ServerAdmin jhonesava123@gmail.com
                WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
                <Directory /var/www/FlaskApp/FlaskApp/>
                        Order allow,deny
                        Allow from all
                </Directory>
                Alias /static /var/www/FlaskApp/FlaskApp/static
                <Directory /var/www/FlaskApp/FlaskApp/static/>
                        Order allow,deny
                        Allow from all
                </Directory>
                ErrorLog ${APACHE_LOG_DIR}/error.log
                LogLevel warn
                CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

====================

  - `sudo a2ensite FlaskApp`
  - `service apache2 reload`

* Almost there... now we just need to configure our WSGI file. To do this:
`cd /var/www/FlaskApp`

===========

`vi flaskapp.wsgi`

* Within the wsgi file, enter:
```
#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FlaskApp/")

from FlaskApp import app as applicatio
================================
```
* `service apache2 restart`


* Then goto your web browser and type the ip address.

Thanks

==========================================================================

* Private Key : `/home/grader/.ssh`
```
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAxMVWJkDkuHWN4RoekKSfvzg5ByTkHrZF04jhpvJ4C7SaOE1S
ybs06nDhmey54q++l//WETvIRVI9SVSPzh8SM+hKLVFRgeqTic1f8/fR1AT8t9YS
qkPuZJNYxe5SDTkUbzuDyRe7ie3FWCn21jxHBKfkcdprXSTA7MfnKGQgRflgSYKY
2wTLY0TTYs4feosd3sG/Dw0jKH+YXQfEBHyxxxivZWcLsg+ZOLv/YXLntbOVHWAt
i5rszLyCv0nbgoS6/sxPOpzPWbKpUDYih16vbMCdDA+zMUDhmqMfw9qf5RIgu38k
8Ok8BPYROd+CdGef6fNr7Kcaulk9ypPkfOTIywIDAQABAoIBACKqiYTvxdvhif9w
dJYTCrnLk/B4RWBLyH1+DhM1gIS/arQkm0NDIg1zmatek1kmkTOCNRqQJ7ZeyMFU
jolH3BMdB4R4YR28UAXlEtSOgn8R6dwRcPRiR2ucsfUdCYOe3MTD/XG+JqIkK7Je
okgYEoL1eT+9tVCRmxOcHFN3YGAzQa/Ez4uN8Xm7mUO9yUn1mv4/mwMMopZxp/Iu
EL/Hk5d6pHd2DNyKp91WSh7z2PcnsDGNj1LM+u8C37H6rost8y1dwXEp2PNplk6f
eyL2E4tDyqteAOUlEUq5IZPBXljDSjdCL34SUuDWzlBSUO0V/TMd6ODtimHzZNWV
BtLjVmECgYEA9EChO6I8BxDmIjFSVqNlFNNvtxV10AZ3Dzb3xUzF/nns+QLfTCBR
tpIaNJYEZsL2ejoAGS0pjoBWFtuXuYsuDJWh6YU8iHqmZvD+OLOHZgMG4R9KG6RJ
wmHNbrAufw2ze41OgxlAqYyfH2jm9EMXkJEv6G8ELM1IS180VQTXBWMCgYEAzjwW
SD0kLp9T8E9ZLE96tkGsYIQhdyk2M6gJGdwc+PFqxXWs8jKLi6W938lNx4WucQWR
/ew0fUubLPIky6zUQbGPLJKU3eFXhJLLrJQApht48swp7/3/+yy4JtX36Rj2jB0b
xhDpP+AGFEqMl/YucMqG2cQt1MtH30kNx8nG33kCgYAKjvSpUEUKBSf9mGY3yo5n
DRDKOEpEeNMSvEyPodb5PioJRZ+Dee4uVzh8x3NfQdRHylQQwowGVfPivxFa+vI9
pwY9wv2v5KVm08oZh2E1/rGAb8rTURHDLlkkDMelxGDa2WvobOIHskV6pR0+t9u/
6xbIFGx4x1L1tyLa/f+RgwKBgQChhjwpbgGlplI2t97urn08u+kHWtVfH978zFH8
eAIVE/f9GXJP6ziSMkipOl/5sgDzMlqqltJxg8LQjAI3p3BC1498aH3B3hkOk26E
BxMPBhtPhooeFkDj951vhUv6u/t1t+Kl2V7mEU6Rm+XLqxuqaWT+sAD5VhE/l1b8
sFNbeQKBgD94GHZ07GTod89dOU9ewBd5oZbbYe2lRdM/VwZav0bgsCqhttwgSbA/
sjJ3YA/gSeqqttUWkKt4uwnWbeD3iRFgTxN6AD/8GcF3HK4kzUKmy21Tx9+6U3qH
smCFU8ec8HNYPGzzWv+GVFTGS0ZVBntGqLgwWmopwN2OIIpQpdiM
-----END RSA PRIVATE KEY-----
```

resources: 
* [ufw](https://www.howtoforge.com/tutorial/ufw-uncomplicated-firewall-on-ubuntu-15-04/)
