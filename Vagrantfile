ISO = "ubuntu/jammy64"

Vagrant.require_version ">= 1.3.5"


Vagrant.configure("2") do |config|
  
  config.vm.box = ISO
  config.vm.box_version = "20240426.0.0"
  config.vm.network "public_network", bridge: "Realtek PCIe GbE Family Controller", use_dhcp_assigned_default_route: true
  config.vm.box_check_update = false
  config.vm.hostname = "ubtjammy.vagrant"
  config.vm.define "vbox-ubt1-jammy64"
  config.vm.synced_folder ".", "/vagrant", type: "smb"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
    vb.name = "vbox-ubt1-jammy64"
  config.vm.provision "shell",  inline: <<-EOF
        export DEBIAN_FRONTEND=noninteractive
        
        sudo apt-get update
        sudo apt-get upgrade -y
        sudo apt-get install -y cifs-utils
      EOF
  end
end

