# Configuring Firewalls by Using RHEL System Roles

Lab by **Justesse Louboulat Milandou** — Second year Cybersecurity (IIBS Dakar)

## Why this lab?

The purpose of this lab is to learn how to automate and standardize firewall
configuration using Ansible and RHEL System Roles. The `firewall` role allows
for a declarative configuration of `firewalld`. The objective is to understand
how to deploy a reproducible firewall configuration on remote machines,
without manually executing every configuration command.

## Prerequisites

- At least 2 VMs on the same network
- One VM compatible with RHEL System Roles (control node)
- `ansible-core` and the `firewall` RHEL System Role installed on the control node

## What this lab covers

1. Installing RHEL System Roles on the control node
2. Building an Ansible inventory (`inventory.yml`) and a playbook (`firewall.yml`)
3. Configuring SSH key-based authentication and `sudo` privilege escalation
4. Enabling the `http` service through `firewalld` via the `firewall` role
5. Opening an arbitrary port (`9999/tcp`) on the managed node
6. Configuring port forwarding (`9999 → 12345`)
7. Resetting the firewall configuration to a clean state (`reset.yml`, `previous: replaced`)
8. Verifying every change with `firewall-cmd --list-all`

## Key takeaway — advantages & trade-offs

The declarative approach of RHEL System Roles offers guaranteed idempotence,
immediate reproducibility across multiple machines, version-controlled
traceability via YAML/Git, and a simple rollback — at the cost of a higher
learning curve, overhead for one-off tasks on a single machine, more
prerequisites (SSH, sudo, Ansible collections), more indirect debugging in
case of failure, and an increased risk of error propagation at scale.
Overall, the value of this approach grows with the number of machines to
manage: marginal on a lab with one or two VMs, but decisive at the scale of
an enterprise server fleet.

## Sources

- https://zero.rhdp.net/lab/zt-rhelbu.zt-firewall-system-role.prod
- https://docs.redhat.com/fr/documentation/red_hat_enterprise_linux/8/html/automating_system_administration_by_using_rhel_system_roles/assembly_configuring-firewalld-using-system-roles_automating-system-administration-by-using-rhel-system-roles
