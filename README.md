[![Travis (.org) branch](https://img.shields.io/travis/nl2go/ansible-role-cloudflare-dns/master)](https://travis-ci.org/nl2go/ansible-role-cloudflare-dns)
[![Ansible Galaxy](https://img.shields.io/badge/role-nl2go.cloudflare_dns-blue.svg)](https://galaxy.ansible.com/nl2go/cloudflare_dns/)
[![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/nl2go/ansible-role-cloudflare-dns)](https://galaxy.ansible.com/nl2go/cloudflare_dns)
[![Ansible Galaxy Downloads](https://img.shields.io/ansible/role/d/46951.svg?color=blue)](https://galaxy.ansible.com/nl2go/cloudflare_dns/)

# Ansible Role: Cloudflare DNS

An Ansible Role that manages [Cloudflare DNS](https://api.cloudflare.com/#dns-records-for-a-zone-properties). Based on the
[cloudflare_dns](https://docs.ansible.com/ansible/latest/modules/cloudflare_dns_module.html), the official Ansible module.

## Prerequisites

- Existing [Cloudflare Account](https://dash.cloudflare.com/sign-up).
- Access to the global API key of the Cloudflare account.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    cloudflare_dns_account_email: average.joe@example.org
 
[Cloudflare] account email.

    cloudflare_dns_account_api_token: 123abc456efg
    
[Cloudflare] account global API token.

    cloudflare_dns_zone: example.org
    
Default target DNS zone.

    cloudflare_dns_records:
      - name: foo
        value: 127.0.0.1

Use `cloudflare_dns_records` to specify custom DNS records.

    cloudflare_dns_records:
      - name: foo
        value: 127.0.0.1
        zone: example.com

Use `zone` to override the DNS zone for a particular DNS entry.

    cloudflare_dns_records:
      - name: foo
        value: 127.0.0.1
        state: absent

Add `state: absent` to ensure a DNS record is removed.

    cloudflare_dns_host_records:
      - name: "{{ inventory_hostname }}"
        value: "{{ hostvars[inventory_hostname].ansible_default_ipv4.address }}"

DNS records for the inventory hosts are created automatically based on the template above.

    cloudflare_dns_all_records: "{{ cloudflare_dns_host_records + cloudflare_dns_records }}"
    
All managed DNS records are combined within the `cloudflare_dns_all_records` variable.

## Tags

Tags can be used to limit the role execution to a particular task module. Following tags are available:

- `cloudflare_dns`,`config`: Covers the full role lifecycle.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
         - nl2go.cloudflare_dns
              
## Development
Use [docker-molecule](https://github.com/nl2go/docker-molecule) following the instructions to run [Molecule](https://molecule.readthedocs.io/en/stable/)
or install [Molecule](https://molecule.readthedocs.io/en/stable/) locally (not recommended, version conflicts might appear).

Provide [Cloudflare] API credentials using environment variables:

    export CLOUDFLARE_DNS_ACCOUNT_EMAIL=average.joe@example.org
    export CLOUDFLARE_DNS_ACCOUNT_API_TOKEN=123abc456efg

Use following to run tests:

    molecule test --all
       
## Maintainers

- [build-failure](https://github.com/build-failure)

## License

See the [LICENSE.md](LICENSE.md) file for details.

## Author Information

This role was created by in 2020 by [Newsletter2Go GmbH](https://www.newsletter2go.com/).

[Cloudflare]:https://www.cloudflare.com/
