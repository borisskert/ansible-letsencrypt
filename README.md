# ansible-letsencrypt

Installs letsencrypt as docker container.

## Requirements

* Python
* Docker

## Tasks

* Create volume paths for docker container
* Create helper scripts
* Setup cron job
* Setup logrotate config
* Create certificates (if not disabled)

## Role parameters

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
| force_cert_creation  | boolean        | no | yes                    | Try to create certificates instantly                                   |

## Example Playbook

### Add to `requirements.yml`:

```yaml
- name: install-letsencrypt
  src: https://github.com/borisskert/ansible-letsencrypt.git
  scm: git
```

Minimal playbook:

```yaml
    - hosts: servers
      roles:
      - install-letsencrypt
```

Typical playbook:

```yaml
    - role: install-letsencrypt
      email: XXXX@gmail.com
      keysize: 4096
      www_volume: /srv/nginx/www
      volume: /srv/letsencrypt
      working_directory: /opt/letsencrypt
      domains:
        - git.myserver.org
        - wiki.myserver.org
      force_cert_creation: yes
```
