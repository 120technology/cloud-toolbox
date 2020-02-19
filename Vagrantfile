Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  
  config.vm.synced_folder ENV["HOME"] + "\\.aws", "/home/vagrant/.aws", type: "smb"

  config.vm.provision "ansible_local" do |ansible|
    ansible.provisioning_path = "/vagrant/provisioning"
    ansible.raw_arguments = ["--verbose"]
    ansible.playbook = "playbook.yaml"
    ansible.extra_vars = {
      tf_version: "0.12.16",
      eksctl_version: "latest_release" # 0.10.2
    }
  end
end
