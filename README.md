# Ansible Role: Mac App Store CLI (mas)

[![Build Status](https://travis-ci.org/kadaan/ansible-role-mas.svg?branch=master)](https://travis-ci.org/kadaan/ansible-role-mas)

Installs [mas](https://github.com/mas-cli/mas) on macOS, and installs macOS apps from the Mac App Store.

## Requirements

  - **Mac App Store account**: You can either sign into the Mac App Store via the GUI before running this role, or you can set the `mas_email` and `mas_password` prior to running the role. For security reasons, if you're going to use this role to sign in, you should use `vars_prompt` for at least the password; don't store unencrypted passwords with your playbooks!

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    mas_email: ""
    mas_password: ""

The credentials for your Mac App Store account. The Apps you install should already be purchased by/registered to this account.

If setting these variables statically (e.g. in an included vars file), you should encrypt the inventory using [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html). Otherwise you can use [`vars_prompt`](http://docs.ansible.com/ansible/playbooks_prompts.html) to prompt for the password at playbook runtime.

If you leave both blank, and don't prompt for them, the role assumes you've already signed in via other means (e.g. via GUI or `mas signin [email]`), and will not attempt to sign in again.

    mas_installed_app_ids: []

A list of apps to ensure are installed on the computer. You can get IDs for all your existing installed apps with `mas list`, and you can search for IDs with `mas search [App Name]`.

    mas_upgrade_all_apps: false

Whether to run `mas upgrade`, which will upgrade all installed Mac App Store apps.

## Dependencies

  - [kadaan.homebrew](https://galaxy.ansible.com/kadaan/homebrew/)

## Example Playbook

    - hosts: localhost
      vars:
        mas_installed_app_ids:
          - 497799835 # Xcode (8.1)
      roles:
        - kadaan.mas

## License

MIT / BSD

## Author Information

[kadaan/ansible-role-homebrew](https://github.com/kadaan/ansible-role-homebrew), 2017 (originally inspired by [Jeff Geerling](https://www.jeffgeerling.com/), 2016).
