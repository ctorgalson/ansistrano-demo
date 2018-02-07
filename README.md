# Ansistrano Demo

This demo uses Ansistrano to deploy a static site with an unprivileged user.

The demo relies on [Vagrant](https://www.vagrantup.com/), the Vagrant plugin
[Vagrant Hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater),
[VirtualBox](https://www.virtualbox.org/), and
[Ansible](https://www.ansible.com/).

The important files are:

- `Vagrantfile`: This boots a Vagrant VM to an initial state with a demo
  website at http://ansistrano-demo.local.
- `provision.yml`: This Ansible playbook runs at `vagrant up` (the first
  time), `vagrant up --provision`, or `vagrant provision`. It handles
  the initial deployment of the demo site.
- `deploy.yml`: This Ansible playbook deploys a changed version of the
  demo site's `index.html` file to the VM via rsync (the changed version
  is located in this repo at `docroot/index.html`).

To test:

1. Run `git clone https://github.com/ctorgalson/ansistrano-demo.git`
2. Run `cd ansistrano-demo && vagrant up`
3. Run `ansible-playbook deploy.yml`
4. Visit http://ansistrano-demo.local in a browser.
5. Run `vagrant ssh` then `cd /var/www/html && ls -hal`.

To retest, change the file at `docroot/index.html` and re-run steps 3 to 5.
