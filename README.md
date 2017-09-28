ansible-beats
=============

Install Elastic Beats data shippers

Requirements
------------

N/A

Role Variables
--------------

* beats_beats: list of beats to install
* beats_filebeat_config: filebeat config yaml
* beats_metricbeat_config: metricbeat config yaml

Dependencies
------------

N/A

Example Playbook
----------------

Define required variables (in the playbook or host_vars). Example:

```
beats_beats:
  - filebeat
  - metricbeat

beats_filebeat_config:
  filebeat.modules:
    - module: system
    - module: nginx
    - module: mysql
  output.elasticsearch:
    hosts: ["myelasticsearchserver.example.com:9200"]

beats_metricbeat_config:
  metricbeat.modules:
    - module: system
      metricsets:
        - cpu
        - load
        - core
        - diskio
        - filesystem
        - fsstat
        - memory
        - network
        - process
        - socket
      enabled: true
      period: 30s
      processes: ['.*']
  output.elasticsearch:
    hosts: ["myelasticsearchserver.example.com:9200"]
```
Example playbook:
```
    - hosts: servers
      roles:
         - { role: artefactual-labs.ansible-beats, tags: ["beats"], become: "yes"}
```
License
-------

AGPLv3

Author Information
------------------

Artefactual Systems
