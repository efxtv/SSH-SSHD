What is ssh? In this post, we are going to see some ssh basic things we need to know. How to generate and connect other Linux computers using SSH connect.

Video Link will be uploaded soon:

# How to install ssh
<pre>sudo apt-get install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh</pre>

#SSH basic command to connect
<pre>ssh user@server-name</pre>
or 
<pre>ssh -p 8022 user@server-name</pre>

#How to generate an ssh config file in .ssh directory
To generate a config file in .ssh directory you need to run the command
 <pre>mkdir ~/.ssh;touch config;ipp=$(ifconfig|grep 192|awk '{print $2}');us=$(whoami);echo -e "\n\n#added by EFX Tv You can change Host, Port if it is different\nhost KaliLinux\nhostname $ipp\nport 22\nuser $us" >>config</pre>
 
 #config file formate
 <pre>host kali
hostname 192.168.1.11
port 2256
user efx
IdentityFile /data/data/com.termux/files/home/.ssh/privatekey.key</pre>

#Permissions .ssh directory and files
<pre>
chmod 700 /home/$USER/.ssh
chmod 644 /home/$USER/.ssh/authorized_keys

#Detailed explain
+------------------------+-------------------------------------+-------------+-------------+
| Directory or File      | Man Page                            | Recommended | Mandatory   |
|                        |                                     | Permissions | Permissions |
+------------------------+-------------------------------------+-------------+-------------+
| ~/.ssh/                | There is no general requirement to  | 700         |             |
|                        | keep the entire contents of this    |             |             |
|                        | directory secret, but the           |             |             |
|                        | recommended permissions are         |             |             |
|                        | read/write/execute for the user,    |             |             |
|                        | and not accessible by others.       |             |             |
+------------------------+-------------------------------------+-------------+-------------+
| ~/.ssh/authorized_keys | This file is not highly sensitive,  | 600         |             |
|                        | but the recommended permissions are |             |             |
|                        | read/write for the user, and not    |             |             |
|                        | accessible by others                |             |             |
+------------------------+-------------------------------------+-------------+-------------+
| ~/.ssh/config          | Because of the potential for abuse, |             | 600         |
|                        | this file must have strict          |             |             |
|                        | permissions: read/write for the     |             |             |
|                        | user, and not accessible by others. |             |             |
|                        | It may be group-writable provided   |             |             |
|                        | that the group in question contains |             |             |
|                        | only the user.                      |             |             |
+------------------------+-------------------------------------+-------------+-------------+
| ~/.ssh/identity        | These files contain sensitive data  |             | 600         |
| ~/.ssh/id_dsa          | and should be readable by the user  |             |             |
| ~/.ssh/id_rsa          | but not accessible by others        |             |             |
|                        | (read/write/execute)                |             |             |
+------------------------+-------------------------------------+-------------+-------------+
| ~/.ssh/identity.pub    | Contains the public key for         | 644         |             |
| ~/.ssh/id_dsa.pub      | authentication.  These files are    |             |             |
| ~/.ssh/id_rsa.pub      | not sensitive and can (but need     |             |             |
|                        | not) be readable by anyone.         |             |             |
+------------------------+-------------------------------------+-------------+-------------+
</pre>

#Change the content of the config file just created. And paste it to the config file in ~/.ssh/config. Or directly run the above command in the directory ~/.ssh/

#How to generate the ssh key for the client you need to connect with?
For example, you want to connect to Kali Linux from Ubuntu. Run the above script in the kali to generate the config file first. Now cat the file and get the IP and user name. After that run the command below from Ubuntu to connect the Kali. (IP for kali and username for kali)
<pre>ssh-keygen 
#hit enter and again do same for two times.
#run the command below to copy the key from Ubuntu to Kali
ssh-copy-id -i ~/.ssh/id_rsa.pub userForKali@IPaddressForKali
or
ssh-copy-id -i ~/.ssh/id_rsa.pub -p 8022 userForKali@IPaddressForKali

</pre>

#How to connect from ubuntu to kali?
Just type ssh and the host example shown below
<pre>ssh kali</pre>

#How to disable the password for incoming connections to get better security?
Go to cd /etc/ssh/ and edit file and mark no to password authentication
nano sshd_config Here you can change the default port and mark no to the root access.
