install-docker-letsencrypt
==========================

Installs letsencrypt as docker container.

Requirements
------------

* Docker
* Nginx

Tasks
-----

* Create volume paths for docker container
* Create helper scripts
* Setup cron job
* Setup logrotate config

Role parameters
--------------

TODO

Example Playbook
----------------

Usage (without parameters):

    - hosts: servers
      roles:
      - install-docker-letsencrypt

Usage (with parameters):

    - hosts: servers
      roles:
      - role: install-docker-letsencrypt
        email: XXXX@gmail.com
        www_volume: /srv/docker/letsencrypt/www
