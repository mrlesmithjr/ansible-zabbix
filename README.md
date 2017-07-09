<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [ansible-zabbix](#ansible-zabbix)
  - [Requirements](#requirements)
  - [Vagrant](#vagrant)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-zabbix

An [Ansible](https://www.ansible.com) role to install/configure [Zabbix](https://www.zabbix.com) Server.

## Requirements

Install required Ansible roles:

```bash
sudo ansible-galaxy install -r requirements.yml -f
```

## Vagrant

Spin up a test environment using Vagrant:

```bash
sudo ansible-galaxy install -r requirements.yml -f
vagrant up
```

Once the environment is up connect to <http://127.0.0.1:8080/zabbix> using
your browswer of choice.
Login using:

    username: Admin
    password: zabbix

You are now ready to begin testing and using Zabbix.
When you are done with your testing you can tear down by:

```bash
./cleanup.sh
```

## Role Variables

```yaml
---
# defaults file for ansible-zabbix

# Define add'l advanced parameters
zabbix_advanced_parameters: []
  # - name: StartVMwareCollectors
  #   value: '{{ zabbix_vmware_instances|int * 2 }}'
  # - name: VMwareCacheSize
  #   value: 8M
  # - name: VMwareFrequency
  #   value: 60
  # - name: VMwarePerfFrequency
  #   value: 60
  # - name: VMwareTimeout
  #   value: 10

zabbix_agent_listen_port: 10050

# Defines if mysql root password should be changed
zabbix_change_mysql_root_password: false

# Defines db info
zabbix_db_info:
  host: 'localhost'
  name: 'zabbix'
  password: 'zabbix'
  port: 3306
  user: 'zabbix'

# Defines pre-req packages for debian
zabbix_debian_pre_req_packages:
  - gzip
  - python-dev
  - python-mysqldb
  - python-pip
  - python-pkg-resources
  - python-setuptools

# Defines Debian based package repo info
zabbix_debian_repo_info:
  package: 'zabbix-release_{{ zabbix_version }}-1+{{ ansible_distribution_release|lower }}_all.deb'
  url: 'http://repo.zabbix.com/zabbix/{{ zabbix_version }}/{{ ansible_distribution|lower }}/pool/main/z/zabbix-release'

# Defines php settings to be added to Apache configuration
zabbix_frontend_php_settings:
  - name: max_execution_time
    value: 300
  - name: memory_limit
    value: 128M
  - name: post_max_size
    value: 16M
  - name: upload_max_filesize
    value: 2M
  - name: max_input_time
    value: 300
  - name: always_populate_raw_post_data
    value: -1
  - name: date.timezone
    value: America/New_York

# Defines which ip info to use in order to add host for monitoring
zabbix_host_interfaces_ip: 'ansible_ssh_host'

# Defines if zabbix groups should be managed
zabbix_manage_groups: false

# Defines if zabbix hosts should be managed
zabbix_manage_hosts: false

# Define mysql root password to be set to if change_mysql_root_password: true
zabbix_mysql_root_password: 'zabbix'

zabbix_mysql_schema_archive: '/usr/share/doc/zabbix-server-mysql/create.sql.gz'

zabbix_python_modules:
  - zabbix-api

# Define zabbix server for agents
zabbix_server: 'node0.{{ pri_domain_name }}'

# List of comma delimited IP addresses that the trapper should listen on
zabbix_server_listen_ip: 0.0.0.0

# Defines Maximum size of log file in MB (0-1024) 0=disable
zabbix_server_logfile_size: 0

zabbix_server_logfile: /var/log/zabbix/zabbix_server.log

# Define zabbix server port
zabbix_server_port: 10051

# Specifies how long we wait for agent
zabbix_server_timeout: 4

zabbix_server_info:
  url: 'http://127.0.0.1/zabbix'
  login_user: 'Admin'
  login_password: 'zabbix'

# Define zabbix version to install (2.2|2.4|3.0)
zabbix_version: 3.0

# Define number of VMware services to monitor (if used)
# vCenter,ESXi hosts and etc.
zabbix_vmware_instances: 1
```

## Dependencies

None

## Example Playbook

[Example Playbook](./playbook.yml)

## License

MIT

## Author Information

Larry Smith Jr.

-   @mrlesmithjr
-   <http://everythingshouldbevirtual.com>
-   mrlesmithjr [at] gmail.com
