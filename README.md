# Cloudflared DNS over HTTPS
Installation for Cloudflared DOH on Raspberry Pi OS. This is an ansible playbook of the documentation found at https://docs.pi-hole.net/guides/dns/cloudflared/#configuring-dns-over-https

# Ansible Galaxy
https://galaxy.ansible.com/ui/standalone/roles/derekpurdy/cloudflared_doh

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
