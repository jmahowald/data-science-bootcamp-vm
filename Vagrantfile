VAGRANTFILE_API_VERSION = "2"

$conda_installation = <<SCRIPT
yum -y install bzip2
curl https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh -o anaconda.sh || exit 1;
bash anaconda.sh -b || exit 1;

grep -q anaconda ~/.bashrc;
if [[ ${?} -ne 0 ]]; then
    echo "export PATH=\"${HOME}/anaconda3/bin:\${PATH}\"" >> ~/.bashrc
fi

source ~/.bashrc

conda info || exit 1;
rm anaconda.sh || exit 1;
conda clean -t || exit 1;

yum clean all || exit 1;

echo '' > ${HOME}/.bash_history
history -c
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"

  config.vm.synced_folder "work", "/workspace"
  config.vm.provision "shell", inline: $conda_installation
end

