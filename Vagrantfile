ISO_Arch = "bento/ubuntu-20.04"

Vagrant.require_version ">= 1.3.5"


Vagrant.configure("2") do |config|
  
  config.vm.box = ISO_Arch
  config.vm.box_version = "202309.09.0"
  config.vm.network "public_network", bridge: "Realtek PCIe GbE Family Controller", use_dhcp_assigned_default_route: true
  config.vm.box_check_update = false
  config.vm.hostname = "ubuntu.vagrant"
  #config.vm.synced_folder ".", "~/vm"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
  config.vm.provision "shell",  inline: <<-EOF
        export DEBIAN_FRONTEND=noninteractive
        # Add Docker's official GPG key:
        sudo apt-get update
        sudo apt-get install ca-certificates curl gnupg
        sudo install -m 0755 -d /etc/apt/keyrings
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
        sudo chmod a+r /etc/apt/keyrings/docker.gpg

        # Add the repository to Apt sources:
        echo \
          "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
          $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
          sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        
        sudo apt-get update
        sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      EOF
  end
end

