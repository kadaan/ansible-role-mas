# Ansible Role: Mac App Store CLI (mas)

[![CI][badge-gh-actions]][link-gh-actions]

Installs [mas](https://github.com/mas-cli/mas) on macOS, and installs macOS apps from the Mac App Store.

## Requirements

  - **Homebrew**: Requires `homebrew` already installed (you can use `geerlingguy.homebrew` to install it on your Mac).
  - **Mac App Store account**: You can either sign into the Mac App Store via the GUI before running this role, or you can set the `mas_email` and `mas_password` prior to running the role. For security reasons, if you're going to use this role to sign in, you should use `vars_prompt` for at least the password; don't store unencrypted passwords with your playbooks!

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    mas_email: ""
    mas_password: ""

The credentials for your Mac App Store account. The Apps you install should already be purchased by/registered to this account.

If setting these variables statically (e.g. in an included vars file), you should encrypt the inventory using [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html). Otherwise you can use [`vars_prompt`](http://docs.ansible.com/ansible/playbooks_prompts.html) to prompt for the password at playbook runtime.

If you leave both blank, and don't prompt for them, the role assumes you've already signed in via other means (e.g. via GUI or `mas signin [email]`), and will not attempt to sign in again.

    mas_signin_dialog: false

Fallback to the built-in Mac App Store dialog to complete sign in. If set to yes, you must specify the aforementioned `mas_email` variable which will be autofilled in the dialog and prompt you to enter your password, followed by the 2FA authorization code if enabled on the account.

    mas_installed_apps:
      - { id: 497799835, name: "Xcode (8.1)" }

A list of apps to ensure are installed on the computer. You can get IDs for all your existing installed apps with `mas list`, and you can search for IDs with `mas search [App Name]`. The `name` attribute is not authoritative and only used to provide better information in the playbook output.

    mas_upgrade_all_apps: false

Whether to run `mas upgrade`, which will upgrade all installed Mac App Store apps.

## Dependencies

  - (Soft dependency) `kadaan.homebrew`

## Example Playbook

    - hosts: localhost
      vars:
        mas_installed_apps:
          - { id: 497799835, name: "Xcode (8.1)" }
      roles:
        - kadaan.homebrew
        - kadaan.mas

## License

MIT / BSD

## Author Information

[kadaan/ansible-role-homebrew](https://github.com/kadaan/ansible-role-homebrew), 2017 (originally inspired by [Jeff Geerling](https://www.jeffgeerling.com/), 2016).

[badge-gh-actions]: https://github.com/kadaan/ansible-role-mas/workflows/CI/badge.svg?event=push
[link-gh-actions]: https://github.com/kadaan/ansible-role-mas/actions?query=workflow%3ACI