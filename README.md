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

   ====================eks cluster nginx============
    yum update -y
    2  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    3   unzip awscliv2.zip
    4  unzip awscliv2.zip
    5  sudo ./aws/install
    6  aws configure
    7  curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    8  sudo mv /tmp/eksctl /usr/local/bin
    9  eksctl version
   10  curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
   11  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
   12  kubectl version --client
   13   ssh-keygen
   15  eksctl create cluster --name arunvel-2 --region us-east-1 --version 1.32 --node-type t2.small --nodes 3 --nodes-min 2 --nodes-max 4 --ssh-access --ssh-public-key /root/.ssh/id_rsa.pub
   16  kubectl get nodes
   17  kubectl get pod
   18  vim nginx.yaml
   20  kubectl apply -f nginx.yaml
   21  kubectl get pod
   22  vim service.yaml
   23  kubectl apply -f service.yaml
   24  kubectl get pod
   25  kubectl get svc

   -----vim nginx----

   apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
-----vim service----

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

=======================terraform vpc=======================
1  sudo dnf install -y dnf-plugins-core
    2  sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
    3  sudo dnf -y install terraform
    4  terraform -v
    5  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    6  unzip awscliv2.zip
    7  sudo ./aws/install
    8  aws configure
    9  cd .aws/
   10  ll
   11  cat config
   12  cat credentials
   13  cd
   14  mkdir terra
   15  cd terra/
   16  ll
   17  vim ec2-vpc.tf
   18  cd
   19  ssh-keygen
   20  cd .ssh/
   21  ll
   22  cat id_rsa.pub
   23  cd
   24  cd terra/
   25  vim ec2-vpc.tf
   26  terraform init
   27  terraform fmt
   28  terraform validate
   29  terraform plan
   30  terraform apply
---------------------------------------------
provider "aws" {
  region = "us-east-1"
 
}
 
#This is VPC code
 
resource "aws_vpc" "test-vpc" {
  cidr_block = "10.0.0.0/16"
}
 
# this is Subnet code
resource "aws_subnet" "public-subnet" {
  vpc_id            = aws_vpc.test-vpc.id
  availability_zone = "us-east-1b"
  cidr_block        = "10.0.0.0/24"
 
  tags = {
    Name = "Public-subnet"
  }
}
 
 
resource "aws_subnet" "private-subnet" {
  vpc_id            = aws_vpc.test-vpc.id
  availability_zone = "us-east-1b"
  cidr_block        = "10.0.1.0/24"
 
  tags = {
    Name = "Private-subnet" #security group
  }
}
 
resource "aws_security_group" "test_access" {
  name        = "test_access"
  vpc_id      = aws_vpc.test-vpc.id
  description = "allow ssh and http"
 
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
 
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
 
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
 
 
}
 
#security group end here#internet gateway code
resource "aws_internet_gateway" "test-igw" {
  vpc_id = aws_vpc.test-vpc.id
 
  tags = {
    Name = "test-igw"
  }
}
 
 
#Public route table code
 
resource "aws_route_table" "public-rt" {
  vpc_id = aws_vpc.test-vpc.id
 
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.test-igw.id
  }
 
 
  tags = {
    Name = "public-rt"
 
  }
}
#route Tatable assosication code
resource "aws_route_table_association" "public-asso" {
  subnet_id      = aws_subnet.public-subnet.id
  route_table_id = aws_route_table.public-rt.id
}
 
#ec2 code
resource "aws_instance" "sanjay-server" {
  ami             = "ami-05ffe3c48a9991133"
  subnet_id       = aws_subnet.public-subnet.id
  instance_type   = "t2.micro"
  security_groups = ["${aws_security_group.test_access.id}"]
  key_name        = "nithya-key"
  tags = {
    Name     = "test-World"
    Stage    = "testing"
    Location = "chennai"
  }
 
}
 
 
##create an EIP for EC2
resource "aws_eip" "sanjay-ec2-eip" {
  instance = aws_instance.sanjay-server.id
}
 
#ssh keypair code
resource "aws_key_pair" "ltimindtree" {
  key_name   = "nithya-new-key"
  public_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCvlb/dvHqB2JMM5s43uWgYsRlUz6eiEz6dX6JvLEZhrN1QbjSyfdsk8bagpohjxLhc2Y0nCD6RjsH5IuuMOEJ05h/KvKI539wEohH7irY7nefho3aVUUPmVlXeytSslIzpOX9CjM/Q4jQbxLMG7AgEEDRZwPyT3fQ3Z0iegKdkwO2R0S5hsyiGFL3gJmMfSn5Oumi20xtiik6L2pHjjN4xk8ozRYMJFVdBAq5a8OiKztqpCDKRMBOAPv46blzLFe5UES4TLIFEaMWXcLhVbdkkqpIO4l6DNq/0FkjR0tYJxghcy/M8TgZ0qqvQhtOQJxmsDL+DCWWZvjuEWJ6Fp8Sbqblo0iBE7DDW0icL+T++qQmjPAs5ODHMUeB67CUEdtFSUVFmhSaI19KpAVpzprbgxXYuFE+hS2bzFThpQriKBDJ6EytQXvRLy7zFigdC78VjQrUJap/JrKpGs1Xdrzqbebcv0N5cCgwivPLlnNimBHEx6AGWKwGucDKGPSVN5L8= root@terraform.example.com"
}
 
###this is database ec2 code
resource "aws_instance" "database-server" {
  ami             = "ami-05ffe3c48a9991133"
  subnet_id       = aws_subnet.private-subnet.id
  instance_type   = "t2.micro"
  security_groups = ["${aws_security_group.test_access.id}"]
  key_name        = "nithya-new-key"
  tags = {
    Name     = "db-World"
    Stage    = "stage-base"
    Location = "delhi"
  }
 
}
 
##create a public ip for Nat gateway
resource "aws_eip" "nat-eip" {
}
### create Nat gateway
resource "aws_nat_gateway" "my-ngw" {
  allocation_id = aws_eip.nat-eip.id
  subnet_id     = aws_subnet.public-subnet.id
}
 
#create private route table
resource "aws_route_table" "private-rt" {
  vpc_id = aws_vpc.test-vpc.id
 
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_nat_gateway.my-ngw.id
  }
 
 
  tags = {
    Name = "private-rt"
  }
}
##route Tatable assosication code
resource "aws_route_table_association" "private-asso" {
  subnet_id      = aws_subnet.private-subnet.id
  route_table_id = aws_route_table.private-rt.id
}
======================================================================================
-----------browser display
 
mkdir user-data
   36  cd user-data
   41  vim user-data.tf
   42  terraform init
   43  terraform fmt
   44  terraform validate
   45  terraform plan
   46  terraform apply
----------------------------------------------
resource "aws_security_group" "web_access23" {
  name        = "web_access23"
  description = "Allow traffic"
  tags = {
    Name = "web_access23"
  }
}
resource "aws_vpc_security_group_ingress_rule" "allow_http" {
  security_group_id = aws_security_group.web_access23.id
  cidr_ipv4         = "0.0.0.0/0"
  from_port         = 80
  ip_protocol       = "tcp"
  to_port           = 80
}
resource "aws_vpc_security_group_ingress_rule" "allow_ssh" {
  security_group_id = aws_security_group.web_access23.id
  cidr_ipv4         = "0.0.0.0/0"
  from_port         = 22
  ip_protocol       = "tcp"
  to_port           = 22
}
resource "aws_vpc_security_group_ingress_rule" "allow_https" {
  security_group_id = aws_security_group.web_access23.id
  cidr_ipv4         = "0.0.0.0/0"
  from_port         = 443
  ip_protocol       = "tcp"
  to_port           = 443
}
resource "aws_vpc_security_group_egress_rule" "allow_all_taraffic" {
  security_group_id = aws_security_group.web_access23.id
  cidr_ipv4         = "0.0.0.0/0"
  ip_protocol       = "-1"
}
#ec2 instance code starts here
resource "aws_instance" "custom-server" {
  ami               = "ami-05ffe3c48a9991133"
  availability_zone = "us-east-1a"
  instance_type     = "t2.micro"
  security_groups   = ["${aws_security_group.web_access23.name}"]
  key_name          = "Milestone-key"

  user_data = <<-EOF
        #!/bin/bash
        sudo yum install httpd -y
        sudo systemctl start httpd
        sudo systemctl enable httpd
        echo "<h1>custom  webserver using terraform</h1>" | sudo tee /var/www/html/index.html
  EOF
  tags = {
    Name     = "hello-India"
    Stage    = "testing"
    Location = "India"
  }
}
===========================================================================================================================
   
