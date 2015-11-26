VAGRANT_API_VERSION = '2'

Vagrant.configure(VAGRANT_API_VERSION) do |config|

  # Base VM OS configuration
  config.vm.box = 'centos/7'

  # Setting the `insert_key` to false will prevent vagrant from generating a
  # new private key, so we can point our Ansible inventory at the common
  # insecure key. Secure keys are less of an issue on local VMs
  config.ssh.insert_key = false

  # VBGuest plugin configuration
  config.vbguest.installer = RedHatGuestAdditionsInstaller

  # VirtualBox configuration
  config.vm.provider :virtualbox do |vb|
    vb.customize [ 'modifyvm', :id, '--memory', 256 ]
    vb.customize [ 'modifyvm', :id, '--cpus', 2 ]
    vb.customize [ 'modifyvm', :id, '--natdnshostresolver1', 'on' ]
    vb.customize [ 'modifyvm', :id, '--ioapic', 'on' ]
    vb.customize [ 'modifyvm', :id, '--ostype', 'RedHat_64' ]
  end

  config.vm.define :centos7 do |app|
    app.vm.hostname = 'centos7'
    app.vm.network :private_network, :ip => '172.20.202.0'
    app.vm.provider :virtualbox do |vb|
      vb.name = "apache-24-scl-centos7"
    end

    app.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", disabled: true
    app.vm.network :forwarded_port, guest: 22, host: 4445, auto_correct: true

    ENV['ANSIBLE_ROLES_PATH'] = File.join(File.dirname(__FILE__), '..')

    app.vm.provision :ansible do |ansible|
      ansible.playbook = 'tests/test.yml'
      ansible.inventory_path = 'tests/vagrant_inventory'
      ansible.limit = 'centos7'
      ansible.verbose = true
      ansible.sudo = true
      ansible.extra_vars = {
          :ansible_ssh_user => 'vagrant',
          :ansible_ssh_private_key_file => '~/.vagrant.d/insecure_private_key',
      }
    end
  end
end

class RedHatGuestAdditionsInstaller < VagrantVbguest::Installers::Linux
  def install(opts = nil, &block)
    communicate.sudo('yum install -y kernel-devel-`uname -r` gcc make perl bzip2', opts, &block)
    super
  end
end
