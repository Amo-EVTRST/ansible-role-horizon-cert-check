# Ansible Role: Horizon Certificate Renewal Checker

This Ansible role allows you to check whether a given certificate can be renewed via the Evertrust Horizon API. It supports searching by either **Distinguished Name (DN)** or **Serial Number** and returns the renewal permission for the target certificate.

---

## Requirements

- Access to the Evertrust Horizon API endpoint
- A valid API account with sufficient rights

---

## API Access Requirements

The API account used (`api_id` / `api_key`) must have the necessary permissions to renew the certificate in question.

## Role Variables

The following variables can be defined when using this role:

| Variable         | Description                                                               | Required | Example                                   |
|------------------|---------------------------------------------------------------------------|----------|-------------------------------------------|
| `horizon_url`     | Horizon API base URL                                                      | ✅        | `https://horizon.amo.esx`                 |
| `api_id`          | Horizon API user ID                                                       | ✅        | `administrator`                           |
| `api_key`         | Horizon API key                                                           | ✅        | `sumBx462MTXUaWyF6a2rZ4GZ`                |
| `cert_identifier` | Either the certificate's DN (starting with `CN=`) or its Serial Number    | ✅        | `CN=www.apple.com` **or** `7413c2...`     |

---

## Example Playbook

```yaml
- name: Check certificate renewal permission
  hosts: localhost
  gather_facts: no
  roles:
    - role: horizon-cert-check
  vars:
    horizon_url: "https://horizon.evertrust.test"
    api_id: "administrator"
    api_key: "sumBx462MTXUaWyF6a2rZ4PT"
    cert_identifier: "CN=www.apple.com"