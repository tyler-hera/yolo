Vagrant.configure("2") do |config|
    config.vm.box = "geerlingguy/ubuntu2004"
    config.vm.provider "virtualbox" do |virtualbox|
       virtualbox.memory = "2048"
       virtualbox.cpus = 2
    end
    config.vm.network "forwarded_port", guest: 80, host: 8080
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end