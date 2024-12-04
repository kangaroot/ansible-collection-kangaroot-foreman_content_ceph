# Ansible collection: kangaroot.foreman_content_ceph

Collection for configuring Ceph repositories in a Foreman/Katello installation.

The Ceph repositories that can be configured from this collection are:

- Ceph Nautilus:
  - EL7
  - EL8[^1]
  - Debian 9
  - Debian 10
  - Ubuntu 18.04 LTS
  - Ubuntu 20.04 LTS

- Ceph Octopus:
  - EL7
  - EL8[^1]
  - Debian 10
  - Ubuntu 18.04 LTS
  - Ubuntu 20.04 LTS

- Ceph Pacific:
  - EL7
  - EL8[^1]
  - EL9[^1]
  - Debian 10
  - Debian 11
  - Ubuntu 18.04 LTS
  - Ubuntu 20.04 LTS

- Ceph Quincy:
  - EL7
  - EL8[^1]
  - EL9[^1]
  - Debian 11
  - Ubuntu 20.04 LTS

- Ceph Reef:
  - EL8[^1]
  - EL9[^1]
  - Debian 11
  - Ubuntu 20.04 LTS
  - Ubuntu 22.04 LTS

- Ceph Squid:
  - EL8[^1]
  - EL9[^1]
  - Debian 11
  - Ubuntu 22.04 LTS

- Ceph Docker images

[^1]: Enabled by default when enabling a specific Ceph release.

## Requirements and Dependencies

Ansible Core 2.13.0 or higher is required for the roles in the collection.

The roles in this collection must be imported by the `kangaroot.foreman` collection. It is possible to directly use the roles in this collection but not recommended.

The `kangaroot.foreman` collection requires the `theforeman.foreman` and `theforeman.operations` collections. To install the required collections, execute:

```shell
ansible-galaxy collection install -r requirements.yml
```

in the collection directory.

## Collection Variables

The `group_vars` directory contains example vars files for the important variables used in the collection roles.

## Usage

The variable `foreman_content_roles` from the `foreman` role in the `kangaroot.foreman` collection contains a list content roles to import.

Add this collection content role to the `foreman_content_roles` list of content roles to import in your playbook project variables.

For example, add the `foreman_content_roles` variable in your `group_vars/foreman.yml` file of your playbook project:

```yaml
# Foreman content roles to include
foreman_content_roles:
  # Package only content
  - kangaroot.foreman_content_ceph.foreman_content_ceph
  - ...

  # OS content
  - kangaroot.foreman_content_rocky.foreman_content_rocky
  - ...

  # Builtin content
  - kangaroot.foreman_content_builtin.foreman_content_builtin
```

Also ensure that the Ceph repositories are enabled and at least one of the Ceph release and/or OS related repositories is enabled as well by setting the appropriate enable variables:

```yaml
foreman_enable_ceph: true
foreman_enable_ceph_squid: true
foreman_enable_ceph_squid_el9: false
```

In your playbook, add a task to execute the `kangaroot.foreman.foreman` role:

```yaml
- name: Run kangaroot.foreman roles
  hosts: foreman
  roles:
    - kangaroot.foreman.foreman
```

