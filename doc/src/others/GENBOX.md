apt-get install squashfs-tools
apt-get install openssh
apt-get install openssh-client
eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa
ssh -T git@github.com
sudo vi /etc/sudoers

Add the line below:

Defaults        env_keep+=SSH_AUTH_SOCK

download : https://portal.frogbywyplay.com/bin/genbox/genbox-latest.run 
chmod +x genbox-latest.run
sudo ./genbox-latest.run
echo 'alias run-genbox="sudo <genbox-dir>/bin/genbox-ng"' >> ~/.bashrc

Copy ssh key to cd genbox/gbx/root/.ssh/
run genbox

emerge --sync
emerge -vDNu world
etc-update


xtarget --sync
xtarget --list-profiles --verbose
xtarget --create -dir=frog --arch=bcm973625sff2l --verbose =product-targets/frog-4.4.3.11
