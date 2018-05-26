ansible-letsencrypt
===================

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

| Variable      | Type | Mandatory? | Default | Description           |
|---------------|------|------------|---------|-----------------------|
| image_name    | text | no         | quay.io/letsencrypt/letsencrypt | Docker image name    |
| image_version | text | no         | latest                          | Docker image version |
| email         | text | yes        |                                 | Your e-mail address  |
| keysize       | text | no         | 4096                            |                      |
| config_volume | path as text | no | /srv/docker/letsencrypt/config  |                      |
| data_volume   | path as text | no | /srv/docker/letsencrypt/data    |                      |
| www_volume    | path as text | no | /srv/docker/letsencrypt/www     |                      |
| script_path          | path as text | no | /opt/letsencrypt         |                      |
| domains              | array of texts | no | []                     | list of your (sub-)domains you want to manage letsencrypt certificates |

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
