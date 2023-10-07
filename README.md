# ansible

A wide collection of Ansible playbooks and roles that are useful

## Setup

Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

```bash
python3 -m pip install --user ansible
```

## Playbooks

### Test

The test playbook is just a sanity check to ensure ansible is working correctly. It's intended to only be used on Debian/Ubuntu systems that use the apt package manager.

```bash
ansible-playbook test.yml
```

### Local

The local install playbook installs commonly used roles that can be found in the `/roles` directory. The playbook currently only supports Debian based systems, however it would be easy to expand support to other Operating Systems using the setup pattern. Here is an example on how RedHat support could be implemented in the `tasks/main.yml`:

```yaml
- include_tasks: setup-RedHat.yml
  when: ansible_os_family == 'RedHat'

- include_tasks: setup-Debian.yml
  when: ansible_os_family == 'Debian'
```

Here RedHat specific tasks could be included in the `tasks/setup-RedHat.yml` file.

To install all roles with the playbook, run the following command:

```bash
ansible-playbook -K local.yml
```

The `-K` flag will prompt for an elevated password since some of these roles require elevated permissions. To limit the scope of what roles to execute, tags can be added to the command:

```bash
ansible-playbook -K local.yml --tags "go,maintenance"
```
