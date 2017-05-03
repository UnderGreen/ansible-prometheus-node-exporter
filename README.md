# Ansible Role: prometheus-node-exporter

An Ansible role that installs Prometheus Node Exporter on Ubuntu|Debian|Redhat-based machines with systemd|Upstart|sysvinit.

## Requirements

All needed packages will be installed with this role.

## Role Variables

Available variables are listed below, along with default values:
```yaml
prometheus_node_exporter_version: 0.14.0

prometheus_node_exporter_enabled_collectors:
  - conntrack
  - cpu
  - diskstats
  - entropy
  - filefd
  - filesystem
  - loadavg
  - mdadm
  - meminfo
  - netdev
  - netstat
  - stat
  - textfile
  - time
  - vmstat

prometheus_node_exporter_config_flags:
  'web.listen-address': '0.0.0.0:9100'
  'log.level': 'info'
```
## Dependencies

- UnderGreen.prometheus-exporters-common

## Example Playbook
```yaml
- hosts: node-exporters
  roles:
    - UnderGreen.prometheus-node-exporter
  vars:
    prometheus_node_exporter_enabled_collectors:
      - diskstats
      - filesystem
      - loadavg
      - systemd
```
## License

GPLv2
