

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
BOX = "generic/ubuntu1804"
GUI_MODE = false
# MAAS Properties
MAAS_MEM = '2024'
# Node Properties
NUM_NODES = 1
NODE_MEM = '1024'


Vagrant.configure("2") do |config|
  # MAAS instance
  config.vm.define "maas", primary: true do |maas|
    maas.vm.box = BOX
    
    maas.vm.hostname = "maascontroller"
    maas.vm.network :private_network, ip: "192.168.50.99"
    maas.vm.network :forwarded_port, guest: 80, host: 5240
    maas.vm.provider :libvirt do |libvirt|
      libvirt.driver = "kvm"
      libvirt.username = "root"
      libvirt.password = "secret"
      libvirt.connect_via_ssh = false
      libvirt.cpu_mode = 'host-passthrough'
      libvirt.memory = '2024'
      libvirt.cpus = 3
      libvirt.storage_pool_name = "default"
    end
    maas.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/maas.yml"
    end
  end

    # Nodes instances
    (1..NUM_NODES).each do |i|
      config.vm.define "node-#{i}" do |node|
          node.vm.box = BOX
          node.vm.network :private_network, ip: "192.168.50.10#{i}"
          node.vm.hostname = "node-#{i}"
          node.vm.provider :libvirt do |libvirt|
            libvirt.boot 'network'
            libvirt.cpu_mode = 'host-passthrough'
            libvirt.memory = NODE_MEM
            libvirt.cpus = '1'
            libvirt.storage :file, :size => '5G', :type => 'qcow2'
          end
  
            node.vm.provision "ansible" do |ansible|
              ansible.playbook = "ansible/node.yml"
            end
      end
  end
end