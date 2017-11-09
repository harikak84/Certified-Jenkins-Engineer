#### 25. Docker Install

```sh
yum remove docker docker-common container-selinux
```

![docker](images/25/1.png)

```sh
yum install yum-utils -y
```

![docker](images/25/2.png)

```sh
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

![docker](images/25/3.png)

```sh
cat /etc/yum.repos.d/docker-ce.repo
```

![docker](images/25/4.png)

```sh
yum clean all
```

![docker](images/25/5.png)

```sh
yum install docker-ce -y
```

![docker](images/25/6.png)

```sh
gpasswd -a jenkins docker
```

![docker](images/25/7.png)

```sh
systemctl start docker
```

![docker](images/25/8.png)

```sh
systemctl restart jenkins
```

![docker](images/25/9.png)

![docker](images/25/10.png)

![docker](images/25/11.png)

![docker](images/25/12.png)

![docker](images/25/13.png)

![docker](images/25/14.png)

![docker](images/25/15.png)

![docker](images/25/16.png)

![docker](images/25/17.png)

![docker](images/25/18.png)

![docker](images/25/19.png)

- Install ``docker`` on ``master``

```sh
yum remove docker docker-common container-selinux
yum install yum-utils -y
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
cat /etc/yum.repos.d/docker-ce.repo
yum clean all
yum install docker-ce -y
gpasswd -a jenkins docker
systemctl start docker
systemctl restart jenkins
```