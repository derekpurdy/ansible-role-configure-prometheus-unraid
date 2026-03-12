# Configuring prometheus.yml on Unraid via Ansible

Configure Prometheus monitoring on Unraid using Ansible, integrating host monitoring targets from your Ansible inventory.

## Features

- Auto-generates `prometheus.yml` from Ansible inventory
- Supports dynamic host discovery with labels
- File service discovery for additional targets (`/etc/prometheus/targets/*.yml`)
- Alertmanager integration
- Docker container restart with validation
- YAML syntax validation before deployment

## Requirements

- Docker installed and running on Unraid
- Prometheus container deployed
- Python 3 with PyYAML (for config validation)

## Role Variables

### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `prometheus_config_dir` | Base directory for Prometheus config | `/mnt/user/appdata/prometheus/etc` |
| `alertmanager_host` | Alertmanager hostname/IP | `alertmanager.lan` |

### Optional Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `prometheus_config_file` | `prometheus.yml.j2` | Template filename |
| `prometheus_port` | `9100` | Node exporter port per host |
| `prometheus_monitored` | `true` | Monitor this host (set to false to skip) |
| `prometheus_container_name` | `prometheus` | Docker container name |
| `alertmanager_port` | `9093` | Alertmanager port |
| `alertmanager_enable_host_down_alert` | `true` | Enable server down alerts |
| `prometheus_env` | *undefined* | Environment label for metrics |

## Usage

### Ansible hosts file

```yaml
---
all:
  children:
    unraid:
      hosts:
        server.lan:
          prometheus_env: 'production'
        backup.lan:
          prometheus_monitored: false  # Skip monitoring this host
```

### Playbook

```yaml
---
- name: Configure Prometheus
  hosts: unraid
  gather_facts: true

  roles:
    - role: derekpurdy.configure_prometheus_unraid
```

### Group variables (group_vars/all/vars.yml)

```yaml
alertmanager_host: 'alertmanager.lan'
alertmanager_port: 9093
prometheus_env: 'production'
```

## Features in Detail

### Dynamic Host Discovery

The role automatically discovers all hosts from your inventory and adds them as scrape targets with customizable labels:
- `hostname`: The Ansible inventory hostname
- `env`: From the `prometheus_env` variable (optional)

Skip monitoring specific hosts by setting `prometheus_monitored: false`.

### File Service Discovery

Additional targets can be added via YAML files in `/etc/prometheus/targets/*.yml`:
```yaml
- targets: ['custom-service:8080']
  labels:
    job: 'custom-service'
```

### Alerting

Server down alerts are enabled by default. Disable with `alertmanager_enable_host_down_alert: false`.

## Ansible Galaxy

https://galaxy.ansible.com/ui/standalone/roles/derekpurdy/configure_prometheus_unraid

## Author

Derek Purdy
