BOX = "ubuntu/jammy64"
BOX_Ver = "20240426.0.0"

#VM_GUEST_PORT = 8080
#VM_HOST_PORT = 8080

#home = ENV['HOME']

Vagrant.require_version ">= 1.3.5"

Vagrant.configure("2") do |config|
  
  config.vm.box = BOX
  config.vm.box_version = BOX_Ver
  config.vm.network "public_network", bridge: "Realtek PCIe GbE Family Controller", use_dhcp_assigned_default_route: true
  #config.vm.network "public_network", bridge: "Realtek PCIe GbE Family Controller", auto_config: false
  #config.vm.network "forwarded_port", guest: VM_GUEST_PORT, host: VM_HOST_PORT 
  config.vm.box_check_update = false
  config.vm.hostname = "ubtjammy.vagrant"
  config.vm.define "vbox-ubt1-jammy64"
  #config.vm.synced_folder ".", "/vagrant", type: "smb"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
    vb.name = "vbox-ubt1-jammy64"
  
  #shell inline provision
  config.vm.provision "shell",  inline: <<-SHELL
      #sudo ip address add 10.0.2.25/24 brd 10.0.2.255 dev enp0s3
      #sudo ip route add default via 10.0.2.1
      sudo apt-get update
      sudo apt full-upgrade --assume-yes
      sudo apt-get install -y apache2 
    SHELL
  end

  #shell file script provision
  config.vm.provision "shell", path: "script.sh" 
   


  #config.vm.provision "ansible" do |ansible|
  #      ansible.playbook = "site.yml"
  #      ansible.verbose = "vv"  
  #end


end



