# -*- mode: ruby -*-
# vi: set ft=ruby :

$docker = <<-SCRIPT
# Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg

    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    sudo apt-get install -y docker-compose
SCRIPT

$dockerc = <<-SCRIPT
# Run Docker Compose
    cd /vagrant
    sudo docker-compose up -d
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64" 
  config.vm.network "public_network", type: "dhcp"
  #config.vm.synced_folder "partage", "/partage"
  #config.vm.provision "file", source: "hosts", destination: "~/" # www.wp.lab
  config.vm.provision "shell", inline: $docker
  config.vm.provision "shell", inline: $dockerc
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = "2"
    #vb.customize ["modifyvm", :id, "--nic1", "none"]
  end
end
