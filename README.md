# practice
--------dev=server t2.micro  8gb
sudo su -
hostnamectl set-hostname dev-server.example.com
bash
yum install git -y
git clone https://github.com/AryanS1508/Aryan_10743412.git
mkdir /project-x
cd aryan/
cp -rvf * /project-x
cd /project-x/
git init, add ., commit -m devops -a
ssh-keygen
cd,cd .ssh/
cat id_rsa.pub copy key git>sshkeygen
cd project-x  create new rep
git init  add commnds form git

-------jenkins t2.medium 12gb

sudo su -
hostnamectl set-hostname jenkins.example.com
bash

cat /etc/os-release
-jenkins on aws copy paste
sudo yum update –y
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
    sudo yum upgrade
    sudo yum install java-17-amazon-corretto -y
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
-open jenkins with the ip from instance need pass copy command
cat / paste command
-copy the password and login
-token from profile save token -rep webhook
-plugin install
yum install maven
yum install git -y
git init
mvn -v 
-cpy path and paste in jdk
new item maven
git url /main

after tomcat
postbuild **/*.war
/
tomcat9 container deployer


----tomcat 

yum install java*
yum install wget
wget
https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.106/bin/apache-tomcat-9.0.106.tar.gz
tar -xvzf a
cd a
cd bin
chmod +x startup.sh
chmod +x shutdown.sh
cd ..
find -name context.xml
vi ./webapps/examples/META-INF/context.xml
vi ./webapps/host-manager/META-INF/context.xml
vi ./webapps/manager/META-INF/context.xml
cd conf
vi tomcat-users.xml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>   
<user username="admin" password="admin" roles="manager-gui,manager-script,manager-jmx,manager-status"/>
<user username="deployer" password="deployer" roles="manager-script"/>
<user username="tomcat" password="s3cret" roles="manager-gui"/>
cd a
cd bin
./startup.sh
ip to url

------------------------------------------userdata

#!/bin/bash
yum install httpd -y
echo "this server is created in aws" >> /var/www/html/index.html
systemctl start httpd
systemctl enable httpd
useradd sanjay -p redhat -c "it works!"

terminal
 1  cd /var/www/html
    2  ll
    3  cat index.html
    4  tail /etc/passwd
    5  tail /etc/shadow

----------------------------------creating an instance create image delete that
create new nst with the ami

same userdata
cd
    8  yum install docker*
    9  yum install vsftpd -y
   10  yum install dns*
   11  yum install nfs-utils -y
   12  yum install cifs-utils -y
   13  touch arun.txt
   14  cat > arun.txt
delete instance create new
check 
ll
rpmquery
---------------------------------server migartion with ami
copy ami send to ohio region
open ohio region create instance from the ami
----------------------------------------storage
create instance
volume > create volume>gp3>5gb>create>action>attach to instance
open instance terminal
ot@ip-172-31-45-76 data]# history
    2  df -h
    4  mkfs.ext4 /dev/xvdb
    7  mkdir /data
    8  mount /dev/xvdb /data
   10  df -h
   11  cd /data
   12  touch arun.txt{1..100}
   13  ll
if we reboot the instance the data gone we nee dto remount 
mount /dev/xvdb /data
to make it permanent -blkid
-copy uuid 
vim /etc/fstab
UUID=8b6c343a-cc26-4c2f-9ff8-3bf7ea0eedf9    /data ext4 defaults 0 0  insert this
systemctl daemon-reload
-------------------------------------change root vol
create inst > vol>modify volme 15gb.
terminal
 1  lsblk
    2  growpart /dev/xvda 1
    7  xfs_growfs /
    8  df -h
-------------------------------------efs storage
create three instance
linux 1a
redhat 1b
ubuntu 1a
aws>efs>create>link>network>manage>change sg>attach>copy link--

linux terminal

 1  yum install nfs-utils -y
    2  mkdir efs
    4 paste link sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 172.31.46.250:/ efs
    5  df -h
    6  cd /root/efs
    7  touch hi.txt{1..10}
    8  ll
redhat

1  yum install nfs-utils -y
    2  systemctl restart nfs-utils
    3  systemctl enable nfs-utils
    4  mkdir efs
    5  sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 172.31.46.250:/ efs
    6  cd /root/efs
    7  ll
ubuntu

1  apt-get update
    2  apt install nfs-common
    3  mkdir efs
    4  sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 172.31.46.250:/ efs
    5  cd /root/efs
    6  ll

------------------------------- to move vol one region to another
create instance in mumbai
create data vol 
attach

-connect instance
sudo su -
lsblk
mkfs.ext4 /etc/sdb
mkdir /data
mount /dev/xvdb /data
df -h
cd /data
touch devops.txt{1..100}
ll

go to snapshot there will be, if not create snap from vol then cpy change region to singapore

-create instance in singapore
-snapshot to vol
-attach to instance
lsblk
mkdir /data
mount /dev/xvdb /data
df -h
cd /data
ll

-------------------------------------------------nat gate

vpc 1      }
int gtw 1
subnet 2    }associate
rt 2
private sub with nat gate
public sub with int gtw
inst http 88, tcp 22

1 yum install httpd -y
2  cd /var/www/html
3  echo "this is my server" >> index.html
4  ll
5  cat index.html
6  systemctl restart httpd
7  systemctl enable httpd
   

---------------------------------------------------vpc big

north v

vpc 1      }
int gtw 1
subnet 2    }associate
rt 2
public sub with int gtw
inst 2
sg http 88, ssh 22, icmp

ohio

vpc 1      }
int gtw 1
subnet 2    }associate
rt 2
public sub with int gtw
inst 2
sg http 88, ssh 22, icmp

public of north v terminal

    1  yum install httpd -y
    2  cd /var/www/html/
    3  echo "this is the server" > index.html
    4  ll
    5  cat index.html
    6  systemctl start httpd
    7  systemctl enable httpd
    9  ping 10.0.1.161 (north v private private ip)
   10  passwd root
   11  vim /etc/ssh/sshd_config --- permitroot login yes,authentication yes
   18  systemctl restart sshd
   19  systemctl enable sshd
   22  cat > arun.txt
   23  ll
   24  scp arun.txt root@18.116.65.23(ohio public public ip):/tmp
   25  ll
   26  cat arun.txt
   27  cd /mnt
   28  ll
   29  cat bala.txt
   30  cd

public of ohio 

 1  yum install httpd -y
    2  ping 20.0.1.210 (ohio private private ip) 
    3  passwd root
    4  vim /etc/ssh/sshd_config
    5  systemctl restart sshd
    6  systemctl enable sshd
    7  cd /tmp
    8  ll
    9  cd
   10  cat > bala.txt
   11  scp bala.txt root@13.217.115.238:/mnt
   12  cd /mnt
   13  ll
   14  cat /mnt
   15  cat bala.txt
   16  ll
   17  cd
   18  ll
before creating mnt
connection peering from n.v to ohio
create peering request from nv to ohio
accept in ohio
NV route table connect public with 20.0.0.0/16
ohio route table connect public with 10.0.0.0/16
------------------

    yum update -y
Search amazon cli …..
   2 curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
    5  yum install python* -y
    6  aws --version
    7  aws configure
    us-east-1
    table
Web repo sanjaygurujiii
    8  sudo yum install automake fuse fuse-devel gcc-c++ git libcurl-devel libxml2-devel make openssl-devel
    9  git clone https://github.com/s3fs-fuse/s3fs-fuse.git
   10  ll
Go to  s3fs-fuse
./configure --prefix=/usr --with-openssl
   15  cd s3fs-fuse
   16  ll
   17  cd autogen.sh
   18  cd /autogen.sh
   19  ./autogen.sh
   20  ./configure --prefix=/usr --with-openssl
   21  make install
   22  cd ..
   23  vim /etc/passwd-s3fs
   24  sudo chmod 640 /etc/passwd-s3fs
   25  s3fs devps59 /mnt -o passwd_file=/etc/passwd-s3fs
   26  df -h
=============================================================
s3 bucket:
create buck > uncheck all > version enable > acls enable > uncheck block all public access
upload file > add > permission > grant public read acess
url of image

iAM :
CREATE USER > attach policies directly > permission - amazon s3 fullaccess > create user
select user > security credentials > access keys > create access > cli > create access key

ec2instance..commands
sudo su -
 1  yum update -y
    2  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    3  unzip awscliv2.zip
    4  sudo ./aws/install
    5  yum install python* -y
    8  aws --version
    9  aws configure
   10  ll
   11  cd .aws/
   14  sudo yum install automake fuse fuse-devel gcc-c++ git libcurl-devel libxml2-devel make openssl-devel
   15  git clone https://github.com/s3fs-fuse/s3fs-fuse.git
   16  ll  
   19  cd  s3fs-fuse
   20  ./autogen.sh
   21  ./configure --prefix=/usr --with-openssl
   22  make
   23  sudo make install
   26  touch /etc/passwd-s3fs
   27  vim /etc/passwd-s3fs
   28  sudo chmod 640 /etc/passwd-s3fs
   29  s3fs 15june25  /mnt -o passwd_file=/etc/passwd-s3fs
   30  df -h
   31  s3fs -o iam_role="s3role" -o url="https://s3-ap-south-1.amazonaws.com" -o endpoint=ap-south-1 -o dbglevel=info -o curldbg -o allow_other -o use_cache=/tmp sanjaynetwork /var/s3fs-demofs
   32  cd /mnt
   34  ll
   35  vim pav.txt
   36  cd
   37  cd /mnt
   38  vim sp.txt
   39  ll
=================================nginx
yum install nginx -y
systemctl start nginx.service
systemctl status nginx.service
yum install docker*
systemctl enable docker
systemctl start docker
docker pull nginx:stable-perl
docker images
docker run -itd --name MyBrowser -p 8080:8080 nginx /bin/bash
docker ps -a
docker attach img id
curl http://localhost
copy the ip and paste in the url


=================================ansible
                                controller
 passwd root
    2  ip a s
    3  vim /etc/hosts
    6  yum install ansible*
    7  scp /etc/hosts root@172.31.11.228:/etc/hosts
    8  ansible --version
    9  ping 172.31.11.228
   10  mkdir -p /etc/ansible
   11  ll -d /etc/ansible/
   12  ll
   13  vim ansible.cfg
   cpy paste from github
   14  ansible --version
   15  ping ans-one.example.com
   16  ssh-keygen
   18  ssh-copy-id root@172.31.11.228
   19  ssh root@ans-one.example.com
   20  ssh root@172.31.11.228
   30  vim /etc/hosts
   31  ansible all -m ping
   32  cd /etc/ansible/
   33  mkdir project-x
   34  cd project-x/
   35  vim simple-playbook.yaml
   cpy from teams bala
   37  ansible-playbook simple-playbook.yaml --syntax-check
   39  cat > index.html
   40  ansible-playbook simple-playbook.yaml

   check in browser with ip of node ip

   =====================worker=======================

    1  passwd root
    2  ip a s
    3  vim /etc/ssh/sshd_config
    4  systemctl start sshd
    5  systemctl enable sshd
    6  vim /etc/ssh/sshd_config
    7  systemctl restart sshd
    8  systemctl enable sshd
    9  hostname
   10  cd /var/www/html
   11  ll
   12  cat index.html
