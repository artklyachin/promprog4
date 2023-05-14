# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.box_url = "Vagrantfile"

  config.vm.provision "file", source: "~/post_configure.sh", destination: ".post_configure.sh"

  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y vim curl 
     apt-get clean
     curl -L https://bootstrap.saltproject.io -o install_salt.sh
     chmod +x install_salt.sh
     ./install_salt.sh -M -P

     chmod +x ./post_configure.sh

     ./post_configure.sh
  SHELL

  config.vm.provision :docker
  config.vm.provision :docker_compose, yml: "/golf-booker/docker-compose.yml",rebuild: true, run: "always"
end
