# ansible-letsencrypt

Installs letsencrypt as docker container.

## Requirements

* Python
* Docker

## Tasks

* Create volume paths for docker container
* Create helper scripts
* Setup cron job
* Create certificates (if not disabled)

## Role parameters

| Variable      | Type | Mandatory? | Default | Description           |
|---------------|------|------------|---------|-----------------------|
| image_name    | text | no         | quay.io/letsencrypt/letsencrypt | Docker image name    |
| image_version | text | no         | latest                          | Docker image version |
| email         | text | yes        |                                 | Your e-mail address  |
| keysize       | text | no         | 4096                            |                      |
| config_volume | path as text | no  | {{volume}}/config |                      |
| data_volume   | path as text | no  | {{volume}}/data   |                      |
| www_volume    | path as text | no  | {{volume}}/www    |                      |
| log_folder    | path as text | no  | /var/log/letsencrypt |                   |
| script_path          | path as text | no | /opt/letsencrypt         |                      |
| sites                | array of `site` | no | []                     | list of your (sub-)domains you want to manage letsencrypt certificates |
| force_cert_creation  | boolean         | no | yes                    | Try to create certificates instantly                                   |

### Definition of `site`

| Property      | Type | Mandatory? | Default | Description           |
|---------------|------|------------|---------|-----------------------|
| domain        | text | yes |      | Defines the domain of the site  |
| dry_run       | boolean | no  |   | Use `--dry-run` switch          |
| test_cert     | boolean | no  |   | use `--test-cert` switch        |
| ignore        | boolean | no  |   | Disable this site               |

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
      sites:
        - domain: git.myserver.org
        - domain: wiki.myserver.org
          dry_run: true
          test_cert: false
          ignore: true
      force_cert_creation: true
```
