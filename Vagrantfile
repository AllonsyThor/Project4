Vagrant.configure("2") do |config|
  config.vm.box = "lazygray/heroku-cedar-14"
  config.vm.network "forwarded_port", guest: 3000, host: 3000, auto_correct: true
  config.vm.provision :shell, :inline => $BOOTSTRAP_SCRIPT # see below
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end
end


$BOOTSTRAP_SCRIPT = <<EOF
  set -e # Stop on any error
  export DEBIAN_FRONTEND=noninteractive

  export LANGUAGE=en_US.UTF-8
  export LANG=en_US.UTF-8
  export LC_ALL=en_US.UTF-8
  locale-gen en_US.UTF-8
  dpkg-reconfigure locales

  echo VAGRANT SETUP: DOING APT-GET STUFF...
  # Install prereqs
  sudo apt-get -y update
  sudo apt-get -y install python-software-properties curl
  sudo apt-get -y install build-essential libssl-dev

  echo ---- NODE ------
  sudo apt-get install -y nodejs-legacy
  cd /vagrant

  rm ~vagrant/.profile

  # Make vagrant automatically go to /vagrant when we ssh in.
  echo "cd /vagrant" | sudo tee -a ~vagrant/.profile

  sudo gem install rails

  echo VAGRANT IS READY.
EOF