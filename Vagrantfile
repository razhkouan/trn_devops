# -*- mode: ruby -*-
# vi: set ft=ruby :
# Author: Aliaksandr Razhkou
# Please use the Vagrant version 1.9.0.

VAGRANTFILE_API_VERSION = "2"

VM_BOX_NAME = "bertvv/centos72"
VM_PROVIDER = "virtualbox"
VM_RAM = "256"

SRV1_NAME = "server_mouse"
SRV1_IP = "10.0.0.10"
SRV1_HOSTNAME = "srvmouse"
SRV1_VM_NETWORK = "private_network"
SRV1_HOSTS_ENTRY = SRV1_IP + "\t\t\t" + SRV1_HOSTNAME

SRV2_NAME = "server_cat"
SRV2_IP = "10.0.0.11"
SRV2_HOSTNAME = "srvcat"
SRV2_VM_NETWORK = "private_network"
SRV2_HOSTS_ENTRY = SRV2_IP + "\t\t\t" + SRV2_HOSTNAME

GIT_REPO_URL = "https://github.com/razhkouan/trn_devops.git"
REPO_NAME = "trn_devops"
BRANCH_NAME = "task1"
README_FILE = "README.md"

$script_change_file_hosts = <<SCRIPT
	sudo echo -e $1 | sudo tee -a /etc/hosts
	sudo echo -e $2 | sudo tee -a /etc/hosts
SCRIPT

$script_task1 = <<SCRIPT
	sudo yum install git -y
	git clone $1
	cd $2
	git checkout $3
	cat $4
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = VM_BOX_NAME
	config.vm.provider VM_PROVIDER do |vb|
		vb.gui = true
		vb.memory = VM_RAM
	end
	config.vm.provision "shell" do |sh|
		sh.inline = $script_change_file_hosts
		sh.args = [SRV1_HOSTS_ENTRY, SRV2_HOSTS_ENTRY]
	end

	config.vm.define SRV1_NAME do |srv1|
		srv1.vm.hostname = SRV1_HOSTNAME
		srv1.vm.network SRV1_VM_NETWORK, ip: SRV1_IP
		srv1.vm.provision "shell" do |sh|
			sh.inline = $script_task1
			# Args [git, git, cd, cat]
			sh.args = [GIT_REPO_URL, REPO_NAME, BRANCH_NAME, README_FILE]
		end
	end
	
	config.vm.define SRV2_NAME do |srv2|
		srv2.vm.hostname = SRV2_HOSTNAME
		srv2.vm.network SRV2_VM_NETWORK, ip: SRV2_IP
		srv2.vm.provision "shell" do |sh|
			sh.inline = "echo '== Ping ==='"
			sh.inline = "ping -c 4 " + SRV1_HOSTNAME
		end
	end
end
