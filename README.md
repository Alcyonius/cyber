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
sudo reboot # As it turns out after some trouble shooting and going back on my previous work, since i am using Ubuntu on VirtualBox i dont seen to have "usernod" as a command, i tried an update again and tried installing "passwd" to no avail so the next part is following the SOC route.
sudo tcpdump -i any -w capture,pcap
wireshark capture.pcap       # Since this is more realistic than a live capture for SOC work so even though usernod isnt a path i can use it's worked in my favour eitherway.

Real-world explanation to this: I workewd within a minimal Ubuntu Linux environment where standard user-management utilities were unavailable, so i performed network traffic capture using elevated privileges and offline PCAP analysis, reflecting real-world SOC workflows.

Lab 4 - Capture traffic using PCAP, analyse, interpret & document:
First we'll capture traffic safely, then analyse in Wireshark.
sudo tcpdump -i any -w lab_capture.pcap        # -i any = captures all interfaces. -w = writes raw traffic tp a PCAP file.
On a second terminal I cause some DNS traffic;
nslookup google.com
I then open firefox on the VM and visit http://example.com & https://google.com to cause some web traffic.
in the second terminal i ping -c 5 8.8.8.8      # ICMP traffic - let this run for 30 seconds.
Back to the original terminal i stopped the capture using CTRL + C which gave me: 16275 packets captured.
wireshark lab_capture.pcap # Opens the capture.
Apply a analysis filter for dns and look for query names, response IPs & unusual domains (length & randomness) # dns analysis
apply icmp as an filter also to look for echo requests / replies and packet timing # icmp analysis
apply http analysis and click a packet > follow > TCP Stream to see plaintext requests, headers & URLs # Which makes HTTP insecure 
Finally we can apply TCP to the same anaysis filter and then go to statistics > conversations > TCP, this shows who talked to whom, how much data moved around & direction of the traffic.   # TCP overview








