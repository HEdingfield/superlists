Provisioning a new site
=======================

## Required packages:

* nginx
* Python 3
* Git
* pip
* virtualenv

eg, on Ubuntu:

    sudo apt-get install nginx git python3 python3-pip
    sudo pip3 install virtualenv

## Nginx Virtual Host config

* see nginx.template.conf
* replace SITENAME with, eg, staging.my-domain.com

e.g.:
elspeth@server:$ sed "s/SITENAME/superlists.ottg.eu/g" \
    deploy_tools/nginx.template.conf | sudo tee \
    /etc/nginx/sites-available/superlists.ottg.eu
elspeth@server:$ sudo ln -s ../sites-available/superlists.ottg.eu \
    /etc/nginx/sites-enabled/superlists.ottg.eu

## Upstart Job

* see gunicorn-upstart.template.conf
* replace SITENAME with, eg, staging.my-domain.com

e.g.:
elspeth@server: sed "s/SITENAME/superlists.ottg.eu/g" \
    deploy_tools/gunicorn-upstart.template.conf | sudo tee \
    /etc/init/gunicorn-superlists.ottg.eu.conf
elspeth@server:$ sudo service nginx reload
elspeth@server:$ sudo start gunicorn-superlists.ottg.eu

## Folder structure:
Assume we have a user account at /home/username

/home/username
└── sites
    └── SITENAME
         ├── database
         ├── source
         ├── static
         └── virtualenv

