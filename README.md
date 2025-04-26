# Install and Configure GUI on an AWS EC2 Ubuntu Instance
Install and Configure GUI on an AWS EC2 Ubuntu Instance

**How to Install and Configure a GUI on an AWS EC2 Instance (Ubuntu)**

**🚩 Problem Statement**

In many cloud-native environments, developers spin up lightweight Ubuntu EC2 instances on AWS for their development tasks. While this setup works great for command-line work, it becomes a limitation when GUI-based tools

are needed.

Recently, our DevOps team was approached by a group of Python developers. Their workflow heavily depends on PyCharm, a popular IDE that offers powerful code navigation, debugging, and project management features. However, 

when they launched their Ubuntu-based EC2 development instances, they realized:

Ubuntu EC2 instances are headless by default, meaning no desktop environment is available.

PyCharm, being a GUI-based tool, requires a graphical interface to function.

They needed a lightweight, performant, and secure GUI setup that wouldn't require re-provisioning or large-scale infrastructure changes.

They turned to the DevOps team to solve this.

**✅ Solution**

As DevOps/SRE professionals, we approached the problem with two goals:

1.** Minimal setup** - Easy to install and maintain.

2. **Remote accessibility** - Developers should be able to access the GUI from their local systems.

🔧 Step-by-Step Guide to Install GUI on an AWS EC2 Ubuntu Instance

Note: All commands are in _Italic_ font only.

1. Login to the development machine: _ssh -i key.pem ubuntu@ip-address-of-ec2-instance_

2. Switch to root user: _sudo su -_

3. Now, to setup and configure GUI, run the following commands in sequence.

_apt update -y

apt upgrade -y

sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

/etc/init.d/ssh restart

adduser username_ #choose a username of your choice and set the password as well

_visudo_

Make an entry in the file similar to this:

![1_oz1NhkhAvcv57rFi6-kQhw](https://github.com/user-attachments/assets/a98fe22d-7570-4483-9436-3a91f1b616ad)

sudoers file to create a superuserSave and quit the file, _:wq + Enter_

_apt install xrdp xfce4 xfce4-goodies tightvncserver -y_

_hostnamectl set-hostname hostgui_ #choose a hostname of your choice

_systemctl restart systemd-hostnamed_

4. Now logout and log back in as root user

_su - username_

_echo xfce4-session> ~/.xsession_

_sudo cp ~/.xsession /etc/skel_

_sudo sed -i '0,/-1/s//ask-1/' /etc/xrdp/xrdp.ini_

_sudo service xrdp restart_

_sudo shutdown -r now_

5. Log back in and become root again:_ sudo su -_
   
_apt-get install putty -y_

6. Now try RDP to the instance with new username and password
   
7. **For RDP:**
   
type windows+R >>>> mstsc >>>> enter ip-address of the instance>>>> user ID and Password

8. This finishes the installation and configuration on GUI on an AWS EC2 Instance
   
YouTube Video URL for step-by-step instructions: https://youtu.be/98b7qNurXyw

![1_SVLEYtCI-hgsBuoNyPmplA](https://github.com/user-attachments/assets/e25e74df-03a0-48d3-a33a-4ff30a7e95ed)

