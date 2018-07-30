Logstash role
=========
[![Build Status](https://api.travis-ci.org/skarj/ansible-role-logstash.svg?branch=master)](https://travis-ci.org/skarj/ansible-role-logstash)

Ansible role for [logstash](https://www.elastic.co/guide/en/logstash/current/introduction.html) 6.x installation.
Versions lower than 6 are not supported by this role.

Requirements
------------

* Ansible 2.5
* This role requires [hash_behaviour=merge](http://docs.ansible.com/ansible/latest/reference_appendices/config.html#default-hash-behaviour) for variables


Dependencies
------------

None


Role Variables
--------------

Default config variables are described in *defaults/main.yml*.
If you need an extended configuration you can specify it in the variables for each environment in section *logstash.config*.
Structure of section *logstash.config* repeats *logstash.yml*, you can insert any parameters described in official logstash [documentation](https://www.elastic.co/guide/en/logstash/current/config-setting-files.html)
Logstash filters and custom patterns are stored in playbook files directory.


Example Playbook
----------------

An example of how to use logstash server role:

        - hosts: all
          roles:
            - role: logstash
              logstash:
                inputs:
                  beats:
                    enabled: true
                  gelf:
                    enabled: false
                  syslog:
                    enabled: false
                  network:
                    enabled: false
                    params:
                      - udp:
                          port: 5000
                          codec: json
                      - tcp:
                          port: 5000
                          codec: json

                outputs:
                  elasticsearch:
                    enabled: true
                    hosts:
                      - 192.168.10.192:9200


License
-------

MIT


Author Information
------------------

Sergey Baranov <skaarj.sergey@gmail.com>
