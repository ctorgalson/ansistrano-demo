VAGRANTFILE_API_VERSION = "2"

# Generate an ssh key for the user `user1`.
system("
  if [ #{ARGV[0]} = 'up' ] && [ ! -f ./keys/user1.pub ]; then
    ssh-keygen -q -b 4096 -N '' -t rsa -f ./keys/user1
  fi
")

# Make sure we have the right plugins.
unless Vagrant.has_plugin?("vagrant-hostsupdater")
  raise "This project requires the `vagrant_hostsupdater` plugin."
end

# Build the VM.
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.network :private_network, ip: "192.168.110.220"
  config.vm.hostname = "ansistrano-demo.local"

  config.vm.provision "shell", inline: "sudo apt install -y python"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision.yml"
  end
end
