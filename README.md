# Ansible Role: Filebeat for ELK Stack

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-filebeat.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-filebeat)

An Ansible Role that installs [Filebeat](https://www.elastic.co/products/beats/filebeat) on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    filebeat_version: 7.x

Supported 6.x and 7.x versions.

Controls the major version of Filebeat which is installed.

    filebeat_create_config: true

Whether to create the Filebeat configuration file and handle the copying of SSL key and cert for filebeat. If you prefer to create a configuration file yourself you can set this to `false`.

### Version 6.x - Prospectors

    filebeat_prospectors:
      - input_type: log
        paths:
          - "/var/log/*.log"

Prospectors that will be listed in the `prospectors` section of the Filebeat configuration. Read through the [Filebeat Prospectors configuration guide](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-options.html) for more options.


### Version 7.x - Inputs and/or modules

    filebeat_modules_enabled: true
    filebeat_modules_path: ${path.config}/modules.d/*.yml

    filebeat_system_log_enabled: true
    filebeat_apache_log_enabled: false
    filebeat_audit_log_enabled: false
    filebeat_elasticsearch_log_enabled: false
    filebeat_haproxy_log_enabled: false
    filebeat_icinga_log_enabled: false
    filebeat_iss_log_enabled: false
    filebeat_iptables_log_enabled: false
    filebeat_kafka_log_enabled: false
    filebeat_kibana_log_enabled: false
    filebeat_logstash_log_enabled: false
    filebeat_mongodb_log_enabled: false
    filebeat_mysql_log_enabled: false
    filebeat_nginx_log_enabled: false
    filebeat_osquery_log_enabled: false
    filebeat_postgresql_log_enabled: false
    filebeat_redis_log_enabled: false
    filebeat_googlesanta_log_enabled: false
    filebeat_suricata_log_enabled: false
    filebeat_traefik_log_enabled: false
    filebeat_zeek_log_enabled: false

    # Filebeat inputs
    filebeat_inputs_enabled: false
    filebeat_inputs:
      - type: log
        paths:
          - "/var/log/*.log"


In 7.x versions,  `prospectors` are replaced by inputs and modules. The 
`inputs` are equivalent to the `prospectors` (See [Filebeat Inputs 
documentation](https://www.elastic.co/guide/en/beats/filebeat/master/configuration-filebeat-options.html)), 
however the `modules` are introduced in this role version with the aim 
of simplifying the configuration of logs of the most common services 
(Sylog, Authlog, Nginx, Apache, MySQL, etc). With the variables show 
above, you can enable and disable the most common Filebeat Modules with 
default configuration. For more options explore [Filebeat Modules 
documentation](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-modules.html).

### Output vars

    filebeat_output_elasticsearch_enabled: true
    filebeat_output_elasticsearch_hosts:
      - "localhost:9200"

Whether to enable Elasticsearch output, and which hosts to send output to.

    filebeat_output_logstash_enabled: true
    filebeat_output_logstash_hosts:
      - "localhost:5000"

Whether to enable Logstash output, and which hosts to send output to.

    filebeat_output_kafka_enabled: true
    filebeat_output_kafka_hosts:
    - "localhost:9092"

Whether to enable Kafka output, and which hosts to send output to.

    filebeat_output_redis_enabled: true
    filebeat_output_redis_hosts:
      - "localhost:6379"

Whether to enable Redis output, and which hosts to send output to.

    filebeat_output_file_enabled: true
    filebeat_output_file_path: /tmp/filebeat
    filebeat_output_file_filename: filebeat

Whether to enable File output, and which hosts to send output to.

    filebeat_output_console_enabled: true

Whether to enable Console output, and which hosts to send output to.

### Logging vars

    filebeat_enable_logging: false
    filebeat_log_level: warning
    filebeat_log_dir: /var/log/filebeat
    filebeat_log_filename: filebeat.log

For configure Filebeat logging.

### SSL vars

    filebeat_ssl_dir: /etc/pki/logstash

The path where certificates and keyfiles will be stored.

    filebeat_ssl_certificate_file: ""
    filebeat_ssl_key_file: ""

Local paths to the SSL certificate and key files, which will be copied into the `filebeat_ssl_dir`.

For utmost security, you should use your own valid certificate and keyfile, and update the `filebeat_ssl_*` variables in your playbook to use your certificate.

To generate a self-signed certificate/key pair, you can use use the command:

    $ sudo openssl req -x509 -batch -nodes -days 3650 -newkey rsa:2048 -keyout filebeat.key -out filebeat.crt

Note that filebeat and logstash may not work correctly with self-signed certificates unless you also have the full chain of trust (including the Certificate Authority for your self-signed cert) added on your server. See: https://github.com/elastic/logstash/issues/4926#issuecomment-203936891

    filebeat_ssl_insecure: "false"

Set this to `"true"` to allow the use of self-signed certificates (when a CA isn't available).

## Dependencies

None.

## Example Playbook

    - hosts: logs
      roles:
        - geerlingguy.java
        - geerlingguy.elasticsearch
        - geerlingguy.logstash
        - geerlingguy.filebeat

## License

MIT / BSD

## Author Information

This role was created in 2016 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
