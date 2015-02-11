# unchained
## virtual django development (batteries included!)

This project is a customized version of torchbox/vagrant-django-template with extra features out of the box and designed to quickly deploy projects to DigitalOcean.

### One-command first-deploy to DigitalOcean
1. Open `deploy.py`
2. Set the DIGITALOCEAN_TOKEN setting to a valid DigitalOcean Personal Access Token with read permissions.
3. Optionally edit any other setting to customize the droplet that will be created.
4. Run `fab first-deploy`. This will create the droplet, deploy your code, and set up NGINX and Gunicorn. This command will also output your site's IP address.
5. Add that IP address to `fabfile.py`.

### fab deploy
1. From then on, run `fab deploy` to update your site on the droplet.

### Feature Overview
* Pre-configured Fabfile for deploying via Git.
* One-command first deploy to a DigitalOcean droplet.
* Vagrantfile for building an Ubuntu Precise based VM
* virtualenv (configured to be active on login), with project dependencies managed through a requirements.txt file
* A PostgreSQL database (with the same name as the project, pre-configured in the project settings file)
* Separation of configuration settings into base.py, dev.py and production.py (and optionally local.py, kept outside of version control)
* django-devserver, django-compressor, django-debug-toolbar
* django-bootstrap3, grappelli, django-braces, django-extensions, and pytz out of the box

### Setup
Install Django 1.7 on your host machine. (Be sure to explicitly uninstall earlier versions first, or use a virtualenv -
having earlier versions around seems to cause pre-1.4-style settings.py and urls.py files to be generated alongside the
new ones.)

To start a new project, run the following commands:

    django-admin.py startproject --template https://github.com/kokeshii/unchained/zipball/master --name=Vagrantfile myproject
    cd myproject
    vagrant up
    vagrant ssh
      (then, within the SSH session:)
    ./manage.py runserver 0.0.0.0:8000

This will make the app accessible on the host machine as http://localhost:8111/ . The codebase is located on the host
machine, exported to the VM as a shared folder; code editing and Git operations will generally be done on the host.
