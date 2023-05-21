IMAGE_NAME = "ubuntu/bionic64"
K8S_NAME = "first-demonstration"

MASTERS_NUM = 1
MASTERS_CPU = 2
MASTERS_MEM = 5120



NODES_NUM_GROUP2 = 4
NODES_CPU_GROUP2 = 4
NODES_MEM_GROUP2 = 5120

NODES_NUM_GROUP3 = 4
NODES_CPU_GROUP3 = 2
NODES_MEM_GROUP3 = 3072

NODES_NUM_GROUP1 = 4
NODES_CPU_GROUP1 = 1
NODES_MEM_GROUP1 = 2048

IP_BASE = "192.168.56."

VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    (1..MASTERS_NUM).each do |i|      
        config.vm.define "k8s-m-#{i}" do |master|
            master.vm.box = IMAGE_NAME
            master.vm.network "private_network", ip: "#{IP_BASE}#{i + 10}"
            master.vm.hostname = "k8s-m-#{i}"
            master.vm.provider "virtualbox" do |v|
                v.memory = MASTERS_MEM
                v.cpus = MASTERS_CPU
		        #v.customize ["modifyhd" , "8712e908-d7b9-4cfb-92fb-3da21a6e9511", "--resize", 10 * 1024] 
                #v.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 0, "--device", 0, "--type", "hdd", "--medium", "/VMs/vms/master.vdi"]
            end            
            master.vm.provision "ansible" do |ansible|
                ansible.playbook = "roles/k8s.yml"
                #Redefine defaults
                ansible.extra_vars = {
                    k8s_cluster_name:       K8S_NAME,                    
                    k8s_master_admin_user:  "vagrant",
                    k8s_master_admin_group: "vagrant",
                    k8s_master_apiserver_advertise_address: "#{IP_BASE}#{i + 10}",
                    k8s_master_node_name: "k8s-m-#{i}",
                    k8s_node_public_ip: "#{IP_BASE}#{i + 10}"
                }                
            end
        end
    end

    (1..NODES_NUM_GROUP1).each do |j|
        config.vm.define "k8s-group1-#{j}" do |node|
	    #node.disksize.size = "10GB"
	    #node.vm.disk :disk, size: "10GB", primary: true
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "#{IP_BASE}#{j + 20}"
            node.vm.hostname = "k8s-group1-#{j}"
            node.vm.provider "virtualbox" do |v|
                v.memory = NODES_MEM_GROUP1
                v.cpus = NODES_CPU_GROUP1
                #v.customize ["createhd", "--filename", "/VMs/vms/node-group1-#{j}.vdi", "--size", 6 * 1024]
                #v.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 0, "--device", 0, "--type", "hdd", "--medium", "/VMs/vms/node-group1-#{j}.vdi"]
                #v.customize ["modifyvm", :id, "--cpuexecutioncap", "20"]
            end             
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "roles/k8s.yml"                   
                #Redefine defaults
                ansible.extra_vars = {
                    k8s_cluster_name:     K8S_NAME,
                    k8s_node_admin_user:  "vagrant",
                    k8s_node_admin_group: "vagrant",
                    k8s_node_public_ip: "#{IP_BASE}#{j + 20}"
                }
            end
        end
    end

    (1..NODES_NUM_GROUP2).each do |j|
        config.vm.define "k8s-group2-#{j}" do |node|
	    #node.disksize.size = "10GB"
	    #node.vm.disk :disk, size: "10GB", primary: true
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "#{IP_BASE}#{j + 30}"
            node.vm.hostname = "k8s-group2-#{j}"
            node.vm.provider "virtualbox" do |v|
                v.memory = NODES_MEM_GROUP2
                v.cpus = NODES_CPU_GROUP2
                #v.customize ["createhd", "--filename", "/VMs/vms/node-group1-#{j}.vdi", "--size", 6 * 1024]
                #v.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 0, "--device", 0, "--type", "hdd", "--medium", "/VMs/vms/node-group1-#{j}.vdi"]
                #v.customize ["modifyvm", :id, "--cpuexecutioncap", "20"]
            end             
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "roles/k8s.yml"                   
                #Redefine defaults
                ansible.extra_vars = {
                    k8s_cluster_name:     K8S_NAME,
                    k8s_node_admin_user:  "vagrant",
                    k8s_node_admin_group: "vagrant",
                    k8s_node_public_ip: "#{IP_BASE}#{j + 30}"
                }
            end
        end
    end


    (1..NODES_NUM_GROUP3).each do |j|
        config.vm.define "k8s-group3-#{j}" do |node|
	    #node.disksize.size = "10GB"
	    #node.vm.disk :disk, size: "10GB", primary: true
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "#{IP_BASE}#{j + 40}"
            node.vm.hostname = "k8s-group3-#{j}"
            node.vm.provider "virtualbox" do |v|
                v.memory = NODES_MEM_GROUP3
                v.cpus = NODES_CPU_GROUP3
                #v.customize ["createhd", "--filename", "/VMs/vms/node-group1-#{j}.vdi", "--size", 6 * 1024]
                #v.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 0, "--device", 0, "--type", "hdd", "--medium", "/VMs/vms/node-group1-#{j}.vdi"]
                #v.customize ["modifyvm", :id, "--cpuexecutioncap", "20"]
            end             
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "roles/k8s.yml"                   
                #Redefine defaults
                ansible.extra_vars = {
                    k8s_cluster_name:     K8S_NAME,
                    k8s_node_admin_user:  "vagrant",
                    k8s_node_admin_group: "vagrant",
                    k8s_node_public_ip: "#{IP_BASE}#{j + 40}"
                }
            end
        end
    end

end
