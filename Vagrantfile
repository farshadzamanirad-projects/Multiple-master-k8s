ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "initializer.sh"

  # Load Balancer Node
  config.vm.define "k8s-lb" do |lb|
    lb.vm.box = "bento/centos-8.2"
    lb.vm.hostname = "k8s-lb"
    lb.vm.network "private_network", ip: "192.168.56.100"
    lb.vm.provider "virtualbox" do |v|
      v.name = "k8s-lb"
      v.memory = 1024
      v.cpus = 1
    end
  end

  MasterCount = 3

  # Kubernetes Master Nodes
  (1..MasterCount).each do |i|
    config.vm.define "k8s-master#{i}" do |mn|
      mn.vm.box = "bento/ubuntu-20.04"
      mn.vm.hostname = "k8s-master#{i}"
      mn.vm.network "private_network", ip: "192.168.56.10#{i}"
      mn.vm.provider "virtualbox" do |v|
        v.name = "k8s-master#{i}"
        v.memory = 2048
        v.cpus = 2
      end
    end
  end

  NodeCount = 2

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "k8s-wn#{i}" do |wn|
      wn.vm.box = "bento/ubuntu-20.04"
      wn.vm.hostname = "k8s-wn#{i}"
      wn.vm.network "private_network", ip: "192.168.56.20#{i}"
      wn.vm.provider "virtualbox" do |v|
        v.name = "k8s-wn#{i}"
        v.memory = 1024
        v.cpus = 1
      end
    end
  end

end
