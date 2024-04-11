Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu2204"
    config.vm.synced_folder ".", "/vagrant" #, mount_options: ["dmode=700,fmode=600"]
    config.vm.provision "shell" do |shell|
        shell.inline = <<-SHELL
            set -euxo pipefail

            # Prevent any interaction from apt:
            export DEBIAN_FRONTEND=noninteractive

            apt-get update

            apt-get install -y virtualbox

            apt-get install -y python3-pip
            pip install ansible
            
            apt-get install -y gnupg software-properties-common curl
            curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add -
            apt-add-repository -S "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main" -y
            apt-get install -y terraform

            mkdir /home/vagrant/terraform
            chown vagrant:vagrant /home/vagrant/terraform
            echo "TF_DATA_DIR=/home/vagrant/terraform" >> /home/vagrant/.bashrc
        SHELL
    end
  end