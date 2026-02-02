Installing Ubuntu using VirtualBox for cyber security learning:
I installed and configured a Linux virtual machine using VirtualBox.
sudo apt update && sudo apt upgrade

I also added Guest Additions CD Image:
Devices > Insert Guest Additions CD Image >
sudo apt install build-essential dkms linux-headers-$(uname -r) 
sudo mount /dev/cdrom /mnt
sudo /mnt/VBoxLinuxAdditions.run
sudo reboot

Lab 1 - Users & Permissions:
whoami: < Displays name >
id: < Displays ID >

I then added a secondary testuser to explore permissions and security as a temporary user:
sudo adduser testuser
sudo usernod -aG sudo testuser
< Log out and log back in as testuser >
sudo apt update # This updates the OS as you were updating an OS for a secondary user as a general admin.



