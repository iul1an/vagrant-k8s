WORKERS = 2
WORKERS == 0 ? (SINGLE_NODE_CLUSTER = true) : (SINGLE_NODE_CLUSTER = false)

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
    config.vm.provider "virtualbox" do |v|
        SINGLE_NODE_CLUSTER ? (v.memory = 4096; v.cpus = 4) : (v.memory = 2048; v.cpus = 2)
    end
    config.vm.define "k8s-master" do |master|
        master.vm.box = "debian/buster64"
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible-playbooks/master-playbook.yaml"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
                metallb_addresses: "192.168.50.100-192.168.50.254",
                single_node_cluster: SINGLE_NODE_CLUSTER
            }
        end
    end
    unless SINGLE_NODE_CLUSTER
        (1..WORKERS).each do |i|
            config.vm.define "k8s-worker-#{i}" do |worker|
                worker.vm.box = "debian/buster64"
                worker.vm.network "private_network", ip: "192.168.50.#{i + 10}"
                worker.vm.hostname = "k8s-worker-#{i}"
                worker.vm.provision "ansible" do |ansible|
                    ansible.playbook = "ansible-playbooks/worker-playbook.yaml"
                    ansible.extra_vars = {
                        node_ip: "192.168.50.#{i + 10}"
                    }
                end
            end
        end
    end
end
