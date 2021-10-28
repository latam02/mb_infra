Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 1200
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.define "ci-server" do |ciserver1|
    ciserver1.vm.network "private_network", ip: '192.168.33.60'
    ciserver1.vm.hostname = "ci-server"
    ciserver1.vm.provision :file, source:"./Docker/docker-compose.ci.yml", destination:"/home/vagrant/docker-compose.yml"
    ciserver1.vm.provision :docker_compose, yml:"/home/vagrant/docker-compose.yml", run:"always"
    ciserver1.vm.provision :shell, inline: "sudo chmod 777 /var/run/docker.sock"
  end


  config.vm.define "cd-server" do |cdserver2|
    cdserver2.vm.network "private_network", ip: '192.168.33.70'
    cdserver2.vm.hostname = "cd-server"
    cdserver2.vm.provision :file, source:"./Docker/docker-compose.cd.yml", destination:"/home/vagrant/docker-compose.yml"
    cdserver2.vm.provision :docker_compose, yml:"/home/vagrant/docker-compose.yml", run:"always"
    cdserver2.vm.provision :shell, inline: "sudo chmod 777 /var/run/docker.sock"
  end

end