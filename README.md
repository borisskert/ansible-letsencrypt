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
| letsencrypt_image_name    | text | no         | quay.io/letsencrypt/letsencrypt | Docker image name    |
| letsencrypt_image_version | text | no         | latest                          | Docker image version |
| letsencrypt_email         | text | yes        |                                 | Your e-mail address  |
| letsencrypt_keysize       | text | no         | 4096                            |                      |
| letsencrypt_config_volume | path as text | no  | {{letsencrypt_volume}}/config |                      |
| letsencrypt_data_volume   | path as text | no  | {{letsencrypt_volume}}/data   |                      |
| letsencrypt_www_volume    | path as text | no  | {{letsencrypt_volume}}/www    |                      |
| letsencrypt_log_folder    | path as text | no  | /var/log/letsencrypt |                   |
| letsencrypt_sites                | array of `site` | no | []                     | list of your (sub-)domains you want to manage letsencrypt certificates |
| letsencrypt_force_cert_creation  | boolean         | no | yes                    | Try to create certificates instantly                                   |

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
      letsencrypt_email: XXXX@gmail.com
      letsencrypt_keysize: 4096
      letsencrypt_www_volume: /srv/nginx/www
      letsencrypt_volume: /srv/letsencrypt
      letsencrypt_working_directory: /opt/letsencrypt
      letsencrypt_sites:
        - domain: git.myserver.org
        - domain: wiki.myserver.org
          dry_run: true
          test_cert: false
          ignore: true
      letsencrypt_force_cert_creation: true
```
