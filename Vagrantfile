Vagrant.configure("2") do |config|
  config.vm.define "web1" do |web1|
    web1.vm.box = "rockylinux/9"
    web1.vm.network "private_network", type: "dhcp"
    web1.vm.network "forwarded_port", guest: 22, host: 2222
    web1.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.inventory_path = "hosts.ini"
      ansible.compatibility_mode = "1.8"
    end
  end

  config.vm.define "web2" do |web2|
    web2.vm.box = "rockylinux/9"
    web2.vm.network "private_network", type: "dhcp"
    web2.vm.network "forwarded_port", guest: 22, host: 2200
    web2.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.inventory_path = "hosts.ini"
      ansible.compatibility_mode = "1.8"
    end
  end
end
