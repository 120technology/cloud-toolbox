Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "toolbox" do |toolbox|

    if Vagrant::Util::Platform.windows?
    then
      toolbox.vm.synced_folder ENV["HOME"] + "\\.aws", "/home/vagrant/.aws", type: "smb"

    elsif (Vagrant::Util::Platform.darwin? || Vagrant::Util::Platform.linux?)
    then
      toolbox.vm.synced_folder ENV["HOME"] + "/.aws", "/home/vagrant/.aws"
    end


    toolbox.vm.provision "ansible_local" do |ansible|
      ansible.provisioning_path = "/vagrant/provisioning"
      # ansible.raw_arguments = ["--verbose"]
      ansible.playbook = "playbook.yaml"
      ansible.extra_vars = {
        tf_version: "0.12.16",
        eksctl_version: "latest_release" # 0.10.2
      }
    end
  end

  config.vm.define "k8s", autostart: false do |k8s|
    k8s.vm.provision "ansible_local" do |ansible|
      ansible.provisioning_path = "/vagrant/provisioning"
      # ansible.raw_arguments = ["--verbose"]
      ansible.playbook = "k8s.yaml"
      ansible.extra_vars = {
        tf_version: "0.12.16",
        eksctl_version: "latest_release" # 0.10.2
      }
    end
  end
end
