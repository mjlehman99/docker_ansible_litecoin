# docker_ansible_litecoin
A simple Dockerized Litecoin Daemon, deployed by ansible

The HOWTO Guide for getting a super simple dockerized Litecoin up and running.

This is configured to do everything "locally". It will still make a ssh connection to localhost.

This is pretty basic as of this writing. Many things can be done make it better.

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

      ansible-playbook litecoins.yml

6.) Check to see if the image built.

      docker image ls

7.) Check to see if it is up and running.

      docker ps -a
