# practice
yum install git -y
git clone https://github.com/AryanS1508/Aryan_10743412.git
mkdir /project-x
cd aryan/
cp -rvf * /project-x
cd /project-x/
git init, add ., commit -m devops -a
ssh-keygen
cd,cd .ssh/
cat id_rsa.pub
cd project-x

git init

jenkins 

cat /etc/os-release

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

cat /
token -rep webhook
plugin
yum install maven
yum install git -y
git init
mvn -v
JDK
new item maven


tomcat 

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
