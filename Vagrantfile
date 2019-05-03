groups = {
  "hello_web" => ["node1"],
  "database" => ["node2"],
  "all_groups:children" => ["hello_web", "database"]
}

Vagrant.configure("2") do |config|
  config.vm.box = "centos7"
  config.vm.define 'node1', autostart: false do |node1|
    node1.vm.network "forwarded_port", guest: 80, host: 8086
    node1.vm.hostname = "node1"
    node1.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provision/playbook.yml"
      ansible.verbose = true
      ansible.groups = groups
    end
  end
  config.vm.define 'node2', autostart: false do |node2|
    node2.vm.hostname = "node2"
    node2.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provision/database.yml"
      ansible.verbose = true
      ansible.groups = groups
    end
  end
  ####### Provision #######
  #config.vm.provision "ansible_local" do |ansible|
  #  ansible.playbook = "provision/playbook.yml"
  #  ansible.limit = "node1"
  #  ansible.verbose = true
  #end
end
