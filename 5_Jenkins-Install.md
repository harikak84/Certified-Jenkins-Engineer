#### 5. Jenkins Install

```sh
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import http://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum install -y jenkins-2.19.4-1.1
```

![jenkins](images/5/1.png)

```sh
yum-config-manager --disable jenkins
```

![jenkins](images/5/2.png)

```sh
systemctl start jenkins
netstat -tulpn | grep 8080
watch n=1 "netstat -tulpn | grep 8080"
```

![jenkins](images/5/3.png)

![jenkins](images/5/4.png)

```sh
systemctl enable jenkins
```

![jenkins](images/5/5.png)

![jenkins](images/5/6.png)

```sh
cat /var/lib/jenkins/secrets/initialAdminPassword
```

![jenkins](images/5/7.png)

![jenkins](images/5/8.png)

![jenkins](images/5/9.png)

![jenkins](images/5/10.png)

![jenkins](images/5/11.png)