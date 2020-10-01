Vagrant.configure("2") do |config|

    config.ssh.insert_key = false
    config.vm.provider "virtualbox" do |v|
        v.cpus = 2
        v.memory = 4096
    end

    (1..3).each do |i|
        config.vm.define "server-#{i}" do |server|
            if i == 1
              INIT = true
              VRRP_STATE = "MASTER"
            else
              INIT = false
              VRRP_STATE = "BACKUP"
            end
            server.vm.box = "debian/buster64"
            server.vm.network "private_network", ip: "192.168.50.#{i + 10}"
            server.vm.hostname = "server-#{i}"
            server.vm.provision "ansible" do |ansible|
                ansible.playbook = "ansible/playbook.yml"
                ansible.extra_vars = {
                    cidr: "192.168.50.0/24",
                    node_ip: "192.168.50.#{i + 10}",
                    vrrp_state: "#{VRRP_STATE}",
                    vrrp_priority: "#{100 - i}",
                    vrrp_interface: "eth1",
                    virtual_ip: "192.168.50.101",
                    apiserver_lb_port: "8443",
                    init: "#{INIT}",
                    metallb_addresses: "192.168.50.150-192.168.50.254",
                }
            end
        end
    end

end
