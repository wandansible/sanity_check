Ansible role: sanity\_check
===========================

Perform sanity checks against the host environment where the
ansible playbook is being run and abandon if any issues are found.

Checks include:

  * Ansible version
  * Required python modules are installed
  * Ansible playbook directory is checked out from the right git branch
    and there are no local changes in the git working tree.

Role Variables
--------------

```
ENTRY POINT: main - Perform sanity checks before running playbooks

        Perform sanity checks against the host environment where the
        ansible playbook is being run and abandon if any issues are
        found. Checks include: ansible version, required python
        modules are installed, ansible playbook directory is checked
        out from the right git branch and there are no local changes
        in the git working tree.

OPTIONS (= is mandatory):

- sanity_check_ansible_playbook_dir
        Path to ansible playbook directory
        default: '{{ ansible_config_file | dirname }}'
        type: str

- sanity_check_git_branch
        Name of the git branch that ansible playbooks should be run
        from
        default: main
        type: str

- sanity_check_git_repo
        If true, run git repo sanity checks against ansible playbook
        directory
        default: true
        type: bool

- sanity_check_minimum_ansible_version
        Minimum ansible version required to run the playbooks
        default: 2.12.0
        type: str

- sanity_check_python_modules
        Python modules required to run the playbooks
        default: [{apt_package: python3-passlib, name: passlib}, {apt_package: python3-jmespath, name: jmespath},
          {apt_package: python3-netaddr, name: netaddr}]
        elements: dict
        type: list

        OPTIONS:

        = apt_package
            Apt package which provides the python module
            type: str

        = name
            Python module name
            type: str
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/sanity_check,main,wandansible.sanity_check

Or, by adding the following to `requirements.yml`:

    - name: wandansible.sanity_check
      src: https://github.com/wandansible/sanity_check

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: all
      roles:
        - role: wandansible.sanity_check
      gather_facts: false
      run_once: true
      become: false
