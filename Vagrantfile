$nodes = <<-EOD
cp -R /vagrant/.ssh ~
EOD

$controller = <<-EOD
echo "$(whoami)@$(hostname)"
date
apt -y update && apt -y install python3 python3-pip
pip3 install ansible virtualenv
ansible --version
EOD

Vagrant.configure('2') do |config|
  config.vm.box = 'ubuntu/bionic64'

  config.vm.define "node1" do |machine|
    #machine.vm.network "private_network", ip: "172.17.177.21"
    config.vm.provision 'shell', inline: $nodes
  end
  
  config.vm.define "node2" do |machine|
    #machine.vm.network "private_network", ip: "172.17.177.22"
    config.vm.provision 'shell', inline: $nodes
  end

  config.vm.define 'controller' do |machine|
    # #machine.vm.network "private_network", ip: "172.17.177.11"

    # machine.vm.provision :ansible_local do |ansible|
    #   # ansible.playbook       = "example.yml"
    #   ansible.verbose        = true
    #   ansible.install        = true
    #   # ansible.limit          = "all" # or only "nodes" group, etc.
    #   # ansible.inventory_path = "inventory"
    config.vm.provision 'shell', inline: $controller
    # end
  end
end
