# Configuring prometheus.yml on a unraid via Ansible using the host list

---

  - Added support for /etc/prometheus/targets/*.yml discovery using file_sd_configs

# Ansible Galaxy
https://galaxy.ansible.com/ui/standalone/roles/derekpurdy/configure_prometheus_unraid

## Ansible hosts file example

    ---

    all:
      children:
        unraid:
          hosts:
            server.lan:

## Ansible Playbook example

    ---

    - name: Playbook for Configuring Prometheus
      hosts: unraid
      gather_facts: yes

      roles:
        - role: derekpurdy.configure_prometheus_unraid

## group_vars/all/vars.yml example
    prometheus_env: 'ENV NAME'
    alertmanager_host: 'alertmanager.lan'

## Author Information
This role was created by Derek Purdy
