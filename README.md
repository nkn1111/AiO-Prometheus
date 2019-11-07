**All In One - Prometheus**
=========

A generic module for setting up the exporter(tested on: node_exporter, blackbox_exporter and kafka_exporter) and the Prometheus and AlertManager itself. Can also be used it any already running Prometheus environment. 

**Requirements**
------------

Works only on systemd linux machines.

**Role Variables**
--------------

Vars which should be set via parameters.

 `app_name:` name of the exporter(should give the official names).

Variables which should be set in special cases.

 `config_path:` Path to the config file, to copy over any config files to the apps config directory.

 `rules_dir:` rules (directory of the rules file, to cp over custom rule files to the prometheus rules config directory. If not will pass the basic rules inside files)

 `git_repo:` prometheus (default to prometheus, have to change for kafka_exporter)


  Example execution:
```---
- hosts: nodes
  roles:
  - role: prometheus-installer
    app_name: node_exporter

- hosts: prometheus
  - role: prometheus-installer
    app_name: prometheus
    rules_dir: "{{ playbook_dir }}/some/directory" ##any .yml file inside this directory will be copied over to the rules directory
    config_path: "{{ playbook_dir }}/some/file"
