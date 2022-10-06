BOX_URL = "https://oracle.github.io/vagrant-projects/boxes"
BOX_NAME = "oraclelinux/8"
VM_NAME = "oracle21c-xe"
VM_MEMORY = "2048"
VM_SYSTEM_TIMEZONE = "Europe/Madrid"
VM_KEEP_DB_INSTALLER = false
VM_ORACLE_CHARACTERSET = "AL32UTF8"
VM_LISTENER_PORT = 1521
VM_EM_EXPRESS_PORT = 5500
VM_ORACLE_PWD = '' # Will be auto-generated when blank



Vagrant.configure("2") do |config|
  config.vm.box = BOX_NAME
  config.vm.box_url = "#{BOX_URL}/#{BOX_NAME}.json"
  config.vm.define VM_NAME
  config.vm.provider "virtualbox" do |v|
    v.memory = VM_MEMORY
    v.name = VM_NAME
  end
  config.vm.provider :libvirt do |v|
    v.memory = VM_MEMORY
  end
  config.vm.hostname = "localhost"
  config.vm.network "forwarded_port", guest: VM_LISTENER_PORT, host: VM_LISTENER_PORT
  config.vm.network "forwarded_port", guest: VM_EM_EXPRESS_PORT, host: VM_EM_EXPRESS_PORT

  # Provision everything on the first run
  config.vm.provision "shell", path: "scripts/install.sh", env:
    {
       "SYSTEM_TIMEZONE"     => VM_SYSTEM_TIMEZONE,
       "KEEP_DB_INSTALLER"   => VM_KEEP_DB_INSTALLER,
       "ORACLE_CHARACTERSET" => VM_ORACLE_CHARACTERSET,
       "LISTENER_PORT"       => VM_LISTENER_PORT,
       "EM_EXPRESS_PORT"     => VM_EM_EXPRESS_PORT,
       "ORACLE_PWD"          => VM_ORACLE_PWD
    }

end
