# Lsa-6050-prac-3-4-5
Lsa practical 3-4-5

practical no: 3 

SSH stands for secured shell .
 The ssh command provides a secure encrypted connection between two hosts over an insecure network.
 This connection can also be used for terminal access, file transfers, and for tunneling other applications.
 
 Commands:
 ->> $sudo apt-get -y install openssh-server
 
 ->> $sudo systemctl enable ssh
 
 (optional)-if required change the configurations from the sshd config file 
 
 ->> $sudo systemctl start ssh
 
 ->> (optional) $sudo systemctl status ssh
 
 ->>$sudo ssh localhost
 
 [then enter your root or user password whatever it may be]
 
 
 practical no : 4 
 
 NFS (Network File System) is basically developed for sharing of files and folders between Linux/Unix systems.
It allows you to mount your local file systems over a network and remote hosts to interact with them as they are mounted locally on the same system. 
With the help of NFS, we can set up file sharing between Unix to Linux system and Linux to Unix system.

There are 4 versions of nfs - nfsv2, nfsv3, nfsv4
NFSv2
--Request are host based and not user based
--TCP or UDP
--supports 2GB file size on clients

NFSv3
--fixes bugs of v2
--TCP or UDP
--Request host based not user based
--support is based on server file limit

NFSv4
--Stateful protocol TCP or SCTCP
--Security features, kerberos
--Client authentication per user basis
--RPC (Remote Procedural Call)
--Listens on port 2049

Commands:-

$sudo apt-get -y install nfs-kernel-server

$sudo systemctl enable nfs-kernel-server

[Create a directory to show the function of nfs i.e(mounting)]

$mkdir demo_dir
$touch a.txt

$cat /etc/exports

[configure your exports file by adding /directory_path/ ipaddr (permissions)]

$sudo exportfs -ra

$sudo apt-get -y install nfs-common

$sudo mount -t nfs /directorytoexport client_ip_ntwrk (permissions) 

[then check for your mounted file in the directory you made]


practical no : 5 

Samba is the standard Windows interoperability suite of programs
 for Linux and Unix.

Since 1992, Samba has provided secure, 
stable and fast file and print services for all clients 
using the SMB/CIFS protocol, such as all versions of 
DOS and Windows, OS/2, Linux and many others.


steps to do samba practical:

install samba
In /home/kali make samba_shared directory
/home/kali/samba_shared me touch a.txt b.txt c.txt
cd /etc/samba
ls /etc/samba
cp smb.conf smb.conf_bkp (for backup)
sudo nano smb.conf
delete all thing inside smb.conf and then write:

[Samba_Shared]
   comment =Welcome to samba
   path = /home/kali/samba_shared
   browseable = yes
   read only = yes

then ctrl x and then y and save 
download smbclient if not there
then do:
sudo systemctl start smbd
sudo systemctl stop nmbd
check both their statuses
do : whoami command
then: sudo pdbedit -a -u $(whoami)
type and retype your passwd
sudo pdbedit -L (to check all users)
sudo ufw allow from 192.168.0.0/16 (or24 my ip was 168.52.128/24) to any app Samba
(this will make any connectionn possible to connect)
check for your ip too : ip a or ip addr
do: sudo ufw reload (will reload your firewall)
you can check your working or not by :
sudo smbcllient -U <username>(mine is kali) -L //your ip
you can also try restarting your smbd and nmbd
sudo systemctl restart smbd/nmbd
and then check their status'
then copy your ip addr and then paste in windows ka run option.
  
  
  
