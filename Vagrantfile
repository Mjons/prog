# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT

export DEBIAN_FRONTEND=noninteractive

composer self-update

#ln -s /etc/apache2/sites-available/localhost-ssl+clients.conf /etc/apache2/sites-enabled/localhost-ssl+clients.conf

service apache2 start
#service mysql start

#mysql -u root -e 'CREATE DATABASE IF NOT EXISTS \`mjp\`;'
#mysql -u root -e 'CREATE USER \`mjp_admin\`@\`localhost\`;'
#mysql -u root -e 'CREATE USER \`mjp_agent\`@\`localhost\`;'
#mysql -u root -e 'GRANT SELECT,UPDATE,DELETE,INSERT ON \`mjp\`.* TO \`mjp_admin\`@\`localhost\`;'
#mysql -u root -e 'GRANT SELECT ON \`mjp\`.* TO \`mjp_agent\`@\`localhost\`;'
#mysql -u root -e 'FLUSH PRIVILEGES;'

#/vagrant/artisan migrate --env=artisan-dev
#/vagrant/artisan db:seed --env=artisan-dev

#rm -r /var/www
#ln -s /vagrant/ /var/www
#echo 'Apache set to serve out of root project folder'

rm -r /var/www
ln -s /vagrant/public/ /var/www
echo "Apache set to serve out of project's public folder"

echo 'Dev server is ready!'

SCRIPT

Vagrant.configure("2") do |config|
	config.vm.box = "jeos64"
	config.vm.box_url = "http://vagrant.orcaweb.ca/jeos64.box"
	# config.vm.box_url = "file:///C:/Users/Barak/VirtualBox%20VMs/jeos64.box"

	config.vm.network :forwarded_port, guest: 80, host: 80, hostip: "127.0.0.1"
	config.vm.network :forwarded_port, guest: 443, host: 443, hostip: "127.0.0.1"
	config.vm.network :forwarded_port, guest: 3306, host: 3306, hostip: "127.0.0.1"

	# Create a private network, which allows host-only access to the machine
	# using a specific IP.
	# config.vm.network :private_network, ip: "192.168.10.10"

	# Create a public network, which generally matched to bridged network.
	# Bridged networks make the machine appear as another physical device on
	# your network.
	# config.vm.network :public_network

	# Share an additional folder to the guest VM. The first argument is
	# the path on the host to the actual folder. The second argument is
	# the path on the guest to mount the folder. And the optional third
	# argument is a set of non-required options.
	# config.vm.synced_folder "../data", "/vagrant_data"

	config.vm.provision :shell, :inline => $script

	# VirtualBox specific settings example
	#
	# config.vm.provider :virtualbox do |vb|
	#   # Don't boot with headless mode
	#   vb.gui = true
	#
	#   # Use VBoxManage to customize the VM. For example to change memory:
	#   vb.customize ["modifyvm", :id, "--memory", "1024"]
	# end
	#
	# View the documentation for the provider you're using for more
	# information on available options.
end
