---
title: Ubuntu 18.04 Common
---

# What to Do after a Fresh Installation

## Basics

### Update `source.list`

+ `Ctrl` + `Alt` + `T` to open up a terminal

  ``` bash
  cd /etc/apt/
  sudo vi sources.list
  ```

+ 不太会用`vi`，但是提供一个最傻瓜的办法

  + Move your cursor to the top of the file, press `I`
  + Press `Enter` 2 times
  + Press `Esc`
  + Move your cursor to the top of the file and press `I` again
  + Copy and Paste the following sources

  ```http
  deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
  ```

+ Press `Esc`

+ Enter `:wq`

### Update your sources

```bash
sudo apt-get update
```

### Upgrade your system(Optional)

+ Note that if you do not wish to used the latest version of ubuntu, **do NOT do this!**

```bash
sudo apt-get upgrade
```

### Create Templates

+ Used to enable `Right Click -> New File` functionality
+ Go to `~/Templates/` or `home/<YourUsername>/Templates`
+ Add template files you need. Examples:
  + `temp.docx`
  + `temp.txt`
  + `readme.md`
  + `temp.xlsx`
  + `temp.pptx`

## Install essential tools

### System Tools

+ Network configuration tools	

  ```bash
  sudo apt-get install net-tools	# This allows your to see your IP address and many other details
  ```

+ Install `openssh-server`

  ```bash
  sudo apt-get install openssh-server	# This allows your computer to be connected via `ssh`	
  ```

+ System Monitors	`htop` & `iotop`

  ```bash
  sudo apt-get install htop	# This allows your to see your system's CPU and Memory usage etc. by each process
  sudo apt-get install iotop	# This allows your to see your system's Disk usage etc. by each process
  ```

+ Nvidia video card driver

  + Search for `drivers` in the search bar
  + Open up `Software & Updates`
  + Select `Additional Drivers`
  + Choose `Using NVIDIA driver metapackage from nvidia-driver-390(proprietary, tested)`

### Version Control Tools

- `Git`

  ```bash
  sudo apt-get install git	# This allows your to use git commands
  ```

### LaTex support

- You will need this if you want to get pretty printed math equations for your pretty docs

  ```bash
  sudo apt-get install texlive-full	# Note that this is kinda large, more than 4 gigs
  ```

### Database

- mysql: Please refer to [Mysql Related](https://askwitionary.github.io/mysql/)

  ```bash
  sudo apt-get install git	# This allows your to use git commands
  ```

## Install your favorite softwares

### A Better txt Editor

- Install `vim` for better command line experience

  ```bash
  sudo apt-get install vim	# This will simply make your life easier	
  ```

+ Install [Typora](https://typora.io/#linux) for easier .md file editting

### IDEA & Conda

+ Please refer to [Setting up Your Coding Environment](https://askwitionary.github.io/python_environment/)
+ If you need `IntelliJ`, the process should be similar

### Install Sogou Pinyin

+ Please refer to [Installing Sogou Pinyin for Ubuntu 18.04](https://askwitionary.github.io/sogou/)

### Database UI

+ Recommendation: [DBeaver](https://dbeaver.io/)



<br>



Everything starts from basics
======

Create a (sudo) user
------

+ Create a user (Needs root privileges)
```bash
sudo adduser lduan
```

+ Follow the steps and fill in your information **(Not Important)**

+ Grant *sudo* privillege to *lduan*
```bash
sudo usermod -aG sudo lduan
```

Create ssh keys and put it onto the server
------

+ Creating your own ssh keys
```bash
ssh-keygen
# And the follow the prompts, normally just keep everything as default.
```

+ Pasting your key to server so that you do not need to enter password each time you login
```bash
cat ~/.ssh/id_rsa.pub
```

+ Copy your key and paste it to the following path on your server
```bash
# if the file does not exist
touch ~/.ssh/authorized_keys
# then
vim ~/.ssh/authorized_keys
```
+ Press `Esc` and `:wq` to save it

Copying files
------

+ Copying files locally
```bash
cp <origin path> <destination path>
# Possible modifiers
# -r regression, copy eveything under the directory
```

+ Copying files using ssh
```bash
scp <username>@<IPaddress>:<path> <destination path>
# Possible modifiers
# -r regression, copy eveything under the directory
# example: copying file to current directory
scp -r md@192.168.164.139:/home/data/ .
```

Checking stats
------

+ Checking disk stats
```bash
lsblk
```

+ Checking file sizes
```bash
du -hs /* Size of all file*/
ls -sh <filename> /* Size of all file*/
ls -sh /* Size of all file*/
ls -l filename /* Size of the file*/
ls -l *        /* Size of All the files in the current directory */
ls -al *       /* Size of All the files including hidden files in the current directory */
ls -al dir/    /* Size of All the files including hidden files in the 'dir' directory */
```

Change command path source
------
+ Resolviing the case where pip and python do not match each other

Networks
======

Setting **Proxy** for `apt`
------

+ Go to `/etc/apt/apt.conf.d/`
``` bash
cd /etc/apt/apt.conf.d/
```

+ Check if a file named `proxy.conf` exists

+ Add/Edit the file as you wish
```bash
# Optional
sudo touch proxy.conf

# Adding proxy configuration
Acquire::http::Proxy "<ProxyServerAddress>:<Port>";
Acquire::https::Proxy "<ProxyServerAddress>:<Port>";

# For instance: 
Acquire::http::Proxy "http://abc.com:61001";

```

Checking speed capability suof network device
------
```bash
cat /sys/class/net/enp4s0/speed
```

Ubuntu 18.04 Desktop ==> Server
======

+ Install Ubuntu 18.04 Desktop normally
	* Use default setup for everything, erase the whole disk to be safe
+ Restart the computer after the installation is complete
+ Remove the installation USB drive
+ Change Ubuntu apt sources to appropriate (fastest) ones
	* Sources provided by Alibaba
```bash
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```
+ Update sources
```bash
sudo apt-get update
```
+ Install openssh-server
```bash
sudo apt-get install openssh-server
```
+ Install net-tools
```bash
sudo apt-get install net-tools
```
+ Edit network settings
	* Check your current IP address `ifconfig`
	* Open wired Internet connection settings
	* Go to IPv4
	* Set IPv4 method to Manual
	* Set IP address you got from the previous step
	* Set Netmask to 255.255.255.1
	* Set Gateway to XXX.XXX.XXX.1
	* Restart web service

Docker Related
======

Installation
------

### Remove older version

``` bash
sudo apt-get remove docker docker-engine docker.io
```

+ Note that this only removes the programs. All the images, containers, volumes and networks under `/var/lib/docker/` are kept.

### Setting up the repository

+ First update the `apt-get` package index
``` bash
sudo apt-get update
```
+ Install packages to allow `apt-get` to use a repository over HTTPS
``` bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

+ Then we can add Docker's official GPG key
``` bash
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
+ **Possible Problem: This Docker link is blocked by the GFW as of 2018.11.06. Try to use proxy if encountered with this problem.**

+ (Optional) Verify that you now have the key with the fingerprint `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88
`
``` bash
sudo apt-key fingerprint 0EBFCD88

pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```

+ Now we can set up the **stable repository**. Note that even if you need development, edge, or test repositories, you always need the stable one. 
``` bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

### Installing Docker CE

+ Update the `apt` package index once again
``` bash
sudo apt-get update
```

+ Install Docker-CE
``` bash
sudo apt-get install docker-ce
```

+ (Optional) Verify your installation
``` bash
sudo docker run hello-world
```

Common commands
------

<br>

### Images

<br>

### Docker

<br>

