# docker_ansible_litecoin
A simple Dockerized Litecoin Daemon, deployed by ansible

The HOWTO Guide for getting a super simple dockerized Litecoin up and running. The litecoind has already been compiled for this example.
If you want to see the compile process, see the notes at the bottom of the page.

This is configured to do everything "locally". It will still make a ssh connection to localhost.

This is pretty basic as of this writing. Many things can be done make it better.
(Add EC2 deployment, compile during the build and deploy process, Monitoring, testing, cleanup of unused docker containers)

Enough talk, lets get some things done here.

Setting up the environment.

Need a linux server with Docker CE, ansible, and git.

1.) Clone the repo down.

      git clone https://github.com/mjlehman99/docker_ansible_litecoin.git

2.) Setup ansible

      Add the following to /etc/ansible/hosts

        [litecoins]
        localhost

3.) Setup ssh keyless access to the user root.

      ssh-keygen (Accept the defaults and leave out the passphrase)
      copy the id_rsa.pub to /root/.ssh/authorized_keys
      chmod 700 /root/.ssh && chmod 600 /root/.ssh/authorized_keys

4.) Test the ssh keyless connection.

      ansible litecoins -m ping

5.) Now run the playbook.

      cd /path_to_where_you_cloned_the_repo/ansible/playbooks
      ansible-playbook litecoins.yml

6.) Check to see if the image built.

      docker image ls

7.) Check to see if it is up and running.

      docker ps -a




## Compile the litecoind for yourself or for some fun.
##### This was done on Ubuntu 14.04

1.) Patch your server.

      apt-get update
      apt-get dist-upgrade
      reboot

2.) Install all the packages needed.

      apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev git npm nodejs nodejs-legacy libminiupnpc-dev redis-server

3.) Added the repo below for the additional packages specific for this coin.

      add-apt-repository ppa:bitcoin/bitcoin
      apt-get update
      apt-get install libdb4.8-dev libdb4.8++-dev

4.) Get the coin source

      git clone https://github.com/litecoin-project/litecoin.git
      cd litecoin
      sudo ./autogen.sh
      sudo ./configure
      sudo make
      sudo make install

5.) Run the Daemon

      cd src
      ./litecoind
