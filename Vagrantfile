#Vagrant.configure("2") do |config|
  
  #образ системы
  #config.vm.box = "ubuntu/trusty64"
  #config.vm.box = "laravel/homestead"
  #config.vm.box = "hashicorp/precise64"
  #config.vm.box = "ubuntu/xenial64"

  #не проверять репозиторий на наличие обновлений 
  #config.vm.box_check_update = false

Vagrant.configure("2") do |config|
  config.vm.box = "laravel/homestead"
  
  config.vm.box_check_update = false
  
   
  ######################################
  config.ssh.insert_key = true
  # имя пользователя
  config.ssh.username = 'vagrant'
  # пароль пользователя
  config.ssh.password = 'vagrant'
  # можно подключаться по паролю
  config.ssh.keys_only = false
  ########################################
  config.vm.network "public_network" 

  config.vm.synced_folder '/home/arkireev', '/vagrant', type: 'rsync'

 # Virtual Machine node-1
 config.vm.define "node1" do |machine|
    machine.vm.network "private_network", ip: "192.168.56.11"
	machine.vm.hostname = "node1"
	machine.vm.network "forwarded_port", guest: 80, host: 8080
	machine.vm.provider "virtualbox" do |vb|
	  vb.name = "VM1"
	  vb.memory = 4096
	  vb.cpus = 3
	end
	
  end
  
  # Virtual Machine node-2
  config.vm.define "node2" do |machine|
    machine.vm.network "private_network", ip: "192.168.56.12"
	machine.vm.hostname = "node2"
	machine.vm.network "forwarded_port", guest: 80, host: 8081
	machine.vm.provider "virtualbox" do |vb|
	  vb.name = "VM2"
	  vb.memory = 3072
	  vb.cpus = 2
	end
	#machine.vm.provision :ansible do |ansible|
	#  ansible.verbose        = "v"
    #  ansible.playbook       = "./playbooks/main.yml"
	  #ansible.galaxy_role_file = "./playbooks/node1_requirements.yml"
      #ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --ignore-certs --force -vvv"
    #  ansible.inventory_path = "./inventory.ini"
    #end
  end
	
  # Virtual Machine node-3
  config.vm.define "node3" do |machine|
    machine.vm.network "private_network", ip: "192.168.56.13"
	machine.vm.hostname = "node3"
	machine.vm.network "forwarded_port", guest: 80, host: 8082
	machine.vm.provider "virtualbox" do |vb|
	  vb.name = "VM3"
	  vb.memory = 2048
	  vb.cpus = 2
	end

    machine.vm.provision :ansible do |ansible|
	  ansible.verbose        = "v"
      ansible.playbook       = "./playbooks/docker_ubuntu.yml"
	  ansible.galaxy_role_file = "./playbooks/node1_requirements.yml"
      #ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --ignore-certs --force -vvv"
      ansible.inventory_path = "./inventory.ini"
    end
	
  end
  
end