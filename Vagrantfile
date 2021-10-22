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
  end


  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: '192.168.33.70'
    server2.vm.hostname = "server-2"
  end

end