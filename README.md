# Mac Development Setup

This Ansible Playbook configures software development environment for my Mac. Based on [geerlingguy/mac-dev-playbook](https://github.com/geerlingguy/mac-dev-playbook), and [ThePrimeagen/ansible](https://github.com/ThePrimeagen/ansible).

## Installation

  1. Ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
  2. Install Ansible:

     - Verify that Pip is installed: `python3 -m pip -V`
     - Install Ansible: `python3 -m pip install --user ansible`
     - Run the following command to add Python 3 to your $PATH: `export PATH="$HOME/Library/Python/3.9/bin:/opt/homebrew/bin:$PATH"`
     - See [Ansible Docs](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible) for details, if needed

  3. Clone this repository: `git clone https://github.com/miksula/mac-setup ~/Projects`
  4. Run `ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles
  5. Run `ansible-playbook main.yml` inside this directory. 

## Use with a remote Mac

You can use this playbook to manage other Macs as well, just make sure you can connect to it with SSH:

  1. (On the Mac you want to connect to:) Go to System Preferences > Sharing.
  2. Enable 'Remote Login'.

You can also enable remote login on the command line:

     sudo systemsetup -setremotelogin on

Then edit the `inventory` file in this repository and change the line that starts with `127.0.0.1` to:

```
[ip/hostname of mac]  ansible_user=[mac ssh username]
```

If you need to supply an SSH password (if you don't use SSH keys), make sure to pass the `--ask-pass` parameter to the `ansible-playbook` command.

## Running a specific set of tagged tasks

You can filter which part of the provisioning process to run by specifying a set of tags using `ansible-playbook`'s `--tags` flag. The tags available are: `personal`.

```
ansible-playbook main.yml -K --tags "personal,other"
```   