# Ansible Role: prometheus-node-exporter

An Ansible role that installs Prometheus Node Exporter on Ubuntu|Debian|Redhat-based machines with systemd|Upstart|sysvinit.

## Requirements

All needed packages will be installed with this role.

## Role Variables

| Variable                                    | Type   | Choices                                                                            | Default                                                                                                                     | Comment                                                                                                                    |
|---------------------------------------------|--------|------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| prometheus_node_exporter_version            | string | See [node_exporter](https://github.com/prometheus/node_exporter/releases) releases | 0.18.1                                                                                                                      | Version of node_exporter that will be installed. Minimal supported version: 0.15                                           |
| prometheus_node_exporter_release_name       | string |                                                                                    | node_exporter-{{ prometheus_node_exporter_version }}.linux-amd64                                                            | Name of the binary that will be downloaed from the   [release](https://github.com/prometheus/node_exporter/releases)  page |
| prometheus_node_exporter_enabled_collectors | list   | [List of flags](https://github.com/prometheus/node_exporter#disabled-by-default)                       | []| List of [collectors that are disabled by default](https://github.com/prometheus/node_exporter#disabled-by-default) to enable                                                                                                  |
| prometheus_node_exporter_disabled_collectors | list   | [List of flags](https://github.com/prometheus/node_exporter#enabled-by-default)                       | []| List of [collectors that are enabled by default](https://github.com/prometheus/node_exporter#enabled-by-default) to disable                                                                                                  |
| prometheus_node_exporter_config_flags       | dict   |                                                                                    |                                                                                                                             | Dict of key, value options to add to the start command line                                                                |
| prometheus_node_exporter_url                | string |                                                                                    | not defined                                                                                                                      | Custom URL to download node_exporter if you can't access to github                                       |


## Dependencies

- UnderGreen.prometheus-exporters-common

## Example Playbook

```yaml
- hosts: node-exporters
  roles:
    - role: undergreen.prometheus-node-exporter
      prometheus_node_exporter_version: 0.18.1
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

## Note:

Due to [prometheus/node_exporter#640](https://github.com/prometheus/node_exporter/pull/640) and [prometheus/node_exporter#639](https://github.com/prometheus/node_exporter/pull/639) changes, this role can only support the minimum version 0.15 of node_exporter.

## License

GPLv2
