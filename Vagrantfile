# Vagrantfile

# Set up Vagrant configuration
Vagrant.configure("2") do |config|
  # Define VMs
  config.vm.define "sender" do |sender|
    sender.vm.box = "ubuntu/bionic64"
    sender.vm.hostname = "sender"
    sender.vm.network "private_network", ip: "192.168.1.10"
  end

  config.vm.define "router" do |router|
    router.vm.box = "ubuntu/bionic64"
    router.vm.hostname = "router"
    router.vm.network "private_network", ip: "192.168.1.11"
  end

  config.vm.define "App1" do |app1|
    app1.vm.box = "ubuntu/bionic64"
    app1.vm.hostname = "App1"
    app1.vm.network "private_network", ip: "192.168.1.12"
  end

  config.vm.define "App2" do |app2|
    app2.vm.box = "ubuntu/bionic64"
    app2.vm.hostname = "App2"
    app2.vm.network "private_network", ip: "192.168.1.13"
  end

  # Provisioning script
  config.vm.provision "shell", inline: <<-SHELL
    # Update repositories and install required packages
    sudo apt-get update
    sudo apt-get install -y iptables

    # Enable IP forwarding
    sudo sysctl -w net.ipv4.ip_forward=1

    # Set up port forwarding from sender to App1 on port 2020
    sudo iptables -t nat -A PREROUTING -p tcp --dport 2020 -j DNAT --to-destination 192.168.1.12:2020
    sudo iptables -t nat -A POSTROUTING -j MASQUERADE
  SHELL
end

