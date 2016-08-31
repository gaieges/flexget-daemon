Flexget Daemon Ansible role
===========================

> Role to set up Flexget in daemon mode

This is a new role, so pull requests and issues are appreciated.

Requirements
------------

- Target to be Ubuntu Xenial
- Ansible 2.2 (still in devel as of 2016-08-28)

Role Variables
--------------

Defaults, override at your own peril:

```yaml
flexget_bind_host: 127.0.0.1
flexget_bind_port: 3539
flexget_enable_ui: yes
flexget_enable_api: yes

flexget_ui_url: "http://{{bind_host}}:{{bind_port}}/ui/"
flexget_api_uri: "http://{{bind_host}}:{{bind_port}}/api/"

flexget_username: flexget
flexget_password: "{{ lookup('pipe','openssl rand -base64 12') }}"

flexget_config_dir: /etc/flexget
flexget_binary: /usr/local/bin/flexget

flexget_system_user: daemon
flexget_system_user_group: daemon

flexget_schedules: 
  - tasks: '*'
    interval:
      minutes: 15

flexget_tasks:
  noop:   # required for initial setup
    manual: yes
```


Example Playbook
----------------

Simply include in your play, pass along variables if desired.  If `flexget_password` is not defined, one will be generated for you.

```yaml
- hosts: all
  become: yes
  roles:
    - role: flexget-daemon
      flexget_password: myPassword

```

License
-------

MIT
