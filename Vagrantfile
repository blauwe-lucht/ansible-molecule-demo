Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu2204"
    config.vm.synced_folder ".", "/vagrant" #, mount_options: ["dmode=700,fmode=600"]

    # Enable nested virtualization:
    config.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--nested-hw-virt", "on"]
    end

    config.vm.provision "shell" do |shell|
        shell.inline = <<-SHELL
            set -euxo pipefail

            # Prevent any interaction from apt:
            export DEBIAN_FRONTEND=noninteractive

            apt-get update

            apt-get install -y virtualbox

            apt-get install -y python3-pip
            pip install ansible

            apt-get install -y vagrant
            
            pip install "molecule[vagrant]"
            pip install molecule-vagrant
            pip install 'molecule-plugins[vagrant]'
        SHELL
    end
  end