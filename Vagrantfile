IMAGE_NAME = "bento/ubuntu-22.04"

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      echo "10.0.0.10  master-node" >> /etc/hosts
      echo "10.0.0.11  worker-node01" >> /etc/hosts
      echo "10.0.0.12  worker-node02" >> /etc/hosts
  SHELL
  
  config.vm.define "master" do |master|
    master.vm.box = IMAGE_NAME
    master.vm.hostname = "master-node"
    master.vm.network "private_network", ip: "10.0.0.10"
    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook/master.yml"
    end
    master.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 2
    end
  end

  # (1..2).each do |i|

  # config.vm.define "node0#{i}" do |node|
  #   node.vm.box = IMAGE_NAME
  #   node.vm.hostname = "worker-node0#{i}"
  #   node.vm.network "private_network", ip: "10.0.0.1#{i}"
  #   node.vm.provider "virtualbox" do |vb|
  #       vb.memory = 2048
  #       vb.cpus = 1
  #   end
  # end
  
  # end
end