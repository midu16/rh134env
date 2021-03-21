VAGRANTFILE_API_VERSION = "2"
VAGRANT_DISABLE_VBOXSYMLINKCREATE = "1"
file_to_disk1 = './disk-0-1.vdi'
file_to_disk2 = './disk-0-2.vdi'
file_to_disk3 = './disk-0-3.vdi'
file_to_disk4 = './disk-0-4.vdi'
file_to_disk11 = './disk-1-1.vdi'
file_to_disk12 = './disk-1-2.vdi'
file_to_disk13 = './disk-1-3.vdi'
file_to_disk14 = './disk-1-4.vdi'
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
# Use same SSH key for each machine
config.ssh.insert_key = false
config.vm.box_check_update = false

# Server 2 Configuration
config.vm.define "node2" do |node2|
  node2.vm.box = "fedora/32-cloud-base"
  node2.vm.box_version = "32.20200422.0"
  node2.vm.hostname = "node2.example.com"
  node2.vm.network "private_network", ip: "10.10.10.202"
  node2.vm.provider "virtualbox" do |node2|
    node2.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 1]

    unless File.exist?(file_to_disk2)
        node2.customize ['createhd', '--filename', file_to_disk2, '--variant', 'Fixed', '--size', 2 * 1024]
      end

      node2.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk2]
    end
end

config.vm.define "node3" do |node3|
  node3.vm.box = "fedora/32-cloud-base"
  node3.vm.box_version = "32.20200422.0"
  node3.vm.hostname = "node3.example.com"
  node3.vm.network "private_network", ip: "10.10.10.203"
  node3.vm.provider "virtualbox" do |node3|
    node3.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 1]

    unless File.exist?(file_to_disk3)
        node3.customize ['createhd', '--filename', file_to_disk3, '--variant', 'Fixed', '--size', 2 * 1024]
      end

      node3.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk3]
    end
end

config.vm.define "node4" do |node4|
  node4.vm.box = "fedora/32-cloud-base"
  node4.vm.box_version = "32.20200422.0"
  node4.vm.hostname = "node4.example.com"
  node4.vm.network "private_network", ip: "10.10.10.204"
  node4.vm.provider "virtualbox" do |node4|
    node4.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 2]

    unless File.exist?(file_to_disk4)
        node4.customize ['createhd', '--filename', file_to_disk4, '--variant', 'Fixed', '--size', 1 * 1024]
      end

      unless File.exist?(file_to_disk14)
        node4.customize ['createhd', '--filename', file_to_disk14, '--variant', 'Fixed', '--size', 1 * 1024]
      end

      node4.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk4]
      node4.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', file_to_disk14]
    end
end

# Controller Configuration
config.vm.define "controller" do |controller|
  controller.vm.hostname = "repo.example.com"
  controller.vm.network "private_network", ip: "10.10.10.200"
  controller.vm.box = "fedora/32-cloud-base"
  controller.vm.box_version = "32.20200422.0"
  controller.vm.hostname = "controller.example.com"
end

# Server 1 Configuration
config.vm.define "node1" do |node1|
  node1.vm.box = "fedora/32-cloud-base"
  node1.vm.box_version = "32.20200422.0"
  node1.vm.hostname = "node1.example.com"
  node1.vm.network "private_network", ip: "10.10.10.201"
end

end
