Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.define "test_app" do |machine|
	machine.vm.network "private_network", ip: "192.168.2.47"
    machine.vm.provision "shell", inline: "apt-get update && apt-get install -y python-minimal"
    machine.vm.provision "ansible", playbook: "git_pull.yml"
    machine.vm.provision "ansible", playbook: "app_deploy.yml"
    machine.vm.provision "ansible", playbook: "app_service.yml"
    machine.vm.provision "ansible", playbook: "nginx_install.yml"
    machine.vm.provision "ansible", playbook: "postgresql_install.yml"
    machine.vm.provision "ansible", playbook: "postgresql.yml"
  end 
end
