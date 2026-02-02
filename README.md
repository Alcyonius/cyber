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

Lab 2 - Linux logs & Security Monitoring:
# View authentication logs
sudo less /var/log/auth.log

# See failed login attempts
sudo grep "Failed password" /var/log/auth.log

# Check sudo usage
sudo grep "sudo" /var/log/auth.log              # From a Cyber Security angle this would be learning how an analyst would detect brute-force login attempts, privilege escalation & Suspicious service activity.

# View recent system logs
journalctl -xe

# See logs from last boot
journalctl -b

Installing a light security monitoring tool:
sudo apt install fail2ban
sudo fail2ban-client status # Checks its status
             # This teaches me automated blocking of malicious IPs, log-based detection & real-world SOC tooling concepts.

Lab 3 - Networking fundamentals + Wireshark:
ip a # Checks IP info
ip route # Checks IP Route
ss -tulnp # Checks open connections
< In this section i used NAT networking in VirtualBox to safely analyse traffic without exposing my host. >
Installing Wireshark:
sudo apt install wireshark
sudo apt usernod -aG wireshark $USER
