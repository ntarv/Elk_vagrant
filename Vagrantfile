# Create a minimal Ubuntu box
Vagrant.require_version ">= 2.1.2"
Vagrant.configure(2) do |config|

    # Configure the base box
    config.vm.define "ubuntu" do |ubuntu|

        # Find the latest images on https://app.vagrantup.com/ubuntu
        ubuntu.vm.box = "ubuntu/bionic64"

        ubuntu.vm.hostname = "elastic-stack"

        ubuntu.vm.network :forwarded_port, guest: 5601, host: 5601
        ubuntu.vm.network :forwarded_port, guest: 80, host: 8880

        # If you export the box switch to the second line to keep the /elastic-stack/ folder
        ubuntu.vm.synced_folder "elk/", "/elk/"
        #ubuntu.vm.synced_folder "elastic-stack/", "/elastic-stack/", type: "rsync"
    end


    # Configure the VirtualBox parameters
    config.vm.provider "virtualbox" do |vb|
        vb.gui = true
        vb.name = "elastic"
        vb.customize [ "modifyvm", :id, "--memory", "4096" ]
    end


    # Configure the box with Ansible
    config.vm.provision "ansible_local" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "elk/0_install.yml"
    end


end
