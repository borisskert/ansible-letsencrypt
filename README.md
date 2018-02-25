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
| log_volume    | path as text | no | /var/log/letsencrypt            |                      |
| www_volume    | path as text | no | /srv/docker/letsencrypt/www     |                      |
| nginx_container_name | text  | no | nginx.service                   | needed to reload nginx after certificate creation or renew |
| script_path          | path as text | no | /opt/letsencrypt         |                                                            |
| logrotate_config     | path as text | no | /etc/logrotate.d/letsencrypt |                                                        |
| cron_job_config      | path as text | no | /etc/cron.d/letsencrypt_renew |                                                       |
| domains              | array of texts | no | []                          | list of your (sub-)domains you want to manage letsencrypt certificates |

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
