# Docker-Study

>In this study, I will go through the basic docker installation, usage, deployment.

Study-plan
- Environment setting





# Environment Setting

I am using google cloud in this project, you will get 300 us dollar credit vaild for one year when you sign-up. 

1. create a project
2. create a VM instance under compute engine, select machine based on your budge, it seems there is option to deploy a docker image directly to this VM, hopefully I can do that after the study.

system CentOS7 (since my work place has rhel, if I have time I will try the same on Ubuntu as well)
Disk 200GB
8 vCPUs
52 GB memory

$250.01 per month (Don't forget to shut down)

For the connection setting, I am using the default one, will look into it if has the time.

Following https://docs.docker.com/engine/installation/linux/docker-ce/centos/ 
all of the following steps are using root
1. enable CentOS extra, should be enabled by default, if not enable it in CentOS-Base.repo in /etc/yum.repos.d/CentOS-Base.repo
```
#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
#baseurl=http://mirror.centos.org/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```
2. remove the old version
```
$ sudo yum remove docker \
                  docker-common \
                  docker-selinux \
                  docker-engine
```

3. installation:
- Most users set up Docker’s repositories and install from them, for ease of installation and upgrade tasks. This is the recommended approach.
> Install required packages. yum-utils provides the yum-config-manager utility, and device-mapper-persistent-data and lvm2 are required by the devicemapper storage driver.
```
$ sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```
> add stable repo
```
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```
> (optional) test edge repo

fill up later

> install
```
sudo yum install docker-ce
```

After install when I check the docker verison by

```
docker version
```

it shows "Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?"

need to use the following command to start the docker

```
service docker start
docker run hello-world
```

- Some users download the RPM package and install it manually and manage upgrades completely manually. This is useful in situations such as installing Docker on air-gapped systems with no access to the internet.

- In testing and development environments, some users choose to use automated convenience scripts to install Docker.

