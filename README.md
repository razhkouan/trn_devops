# trn_devops
The repository contains tasks and the results of their implementation.

Task for Module 1
1.	Create Github account
2.	Create Github repository (for example “training”)
3.	Create branch task1 (commit some text file into this branch)
4.	Install VirtualBox with extensions
5.	Install Vagrant
6.	Create Vagrantfile based on Centos7 distributive (vagrant box can be used the same as in presentation)
7.	Bring up and provision several VMs (2 is enough) with “Shell” provisioner:
		- install git on only one of them
		- clone your repository on machine where git is installed and checkout “task1” branch, print to console content of text file from item 3.
		- ping between machines should work via DNS names
8.	Commit Vagrantfile into “task1” branch.