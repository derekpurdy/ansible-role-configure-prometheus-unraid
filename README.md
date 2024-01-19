# Configuring prometheus.yml on a unraid via Ansible using the host list
Configure prometheus.yml file on Unraid via Ansible using the host list

# Ansible Galaxy
[https://galaxy.ansible.com/ui/standalone/roles/derekpurdy/cloudflared_doh](https://galaxy.ansible.com/ui/standalone/roles/derekpurdy/configure_prometheus_unraid/)

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


## Author Information
This role was created by Derek Purdy
