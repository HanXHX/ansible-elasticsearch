# -*- mode: ruby -*-
# vi: set ft=ruby :
# vi: set tabstop=2 :
# vi: set shiftwidth=2 :

Vagrant.configure("2") do |config|

	vms = [
		[ "node1", "debian/jessie64" ],
		[ "node2", "debian/jessie64" ],
		[ "node3", "debian/jessie64" ]
	]

	config.vm.provider "virtualbox" do |v|
		v.cpus = 1
		v.memory = 512
	end

	vms.each do |vm|
		config.vm.define vm[0] do |m|
			m.vm.hostname = vm[0]
			m.vm.box = vm[1]
			m.vm.network "private_network", type: "dhcp"
			m.vm.provision "ansible" do |ansible|
				ansible.playbook = "tests/vagrant.yml"
				ansible.verbose = 'vv'
				ansible.sudo = true
			end
		end
	end
end
