# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
	# Base box to build off, and download URL for when it doesn't exist on the user's system already
	config.vm.box = "precise32"
	config.vm.box_url = "http://files.vagrantup.com/precise32.box"

	# Forward a port from the guest to the host, which allows for outside
	# computers to access the VM, whereas host only networking does not.
	config.vm.forward_port 8000, 8111
	
	# Share an additional folder to the guest VM. The first argument is
	# an identifier, the second is the path on the guest to mount the
	# folder, and the third is the path on the host to the actual folder.
	config.vm.share_folder "project", "/home/vagrant/{{ project_name }}", "."
	
	# Enable provisioning with a shell script.
	config.vm.provision :shell, :path => "etc/install/install.sh", :args => "{{ project_name }}"
	
end
