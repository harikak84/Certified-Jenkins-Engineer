#### 11. Exercise: Install a Jenkins Master and Prerequisites

######  Prerequisite Install

- Download [Java](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

- Copy the package from your local environment to the target server

```sh
scp jdk-8u121-linux-x64.rpm user@your-server:/home/user/
```

- Install the jdk package

```sh
rpm -Uvh jdk-8u121-linux-x64.rpm
```

- Set up alternatives for Java

```sh
alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000
alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000
```

- Set ``JAVA_HOME`` environmental variable in ``rc.local``

```sh
vi /etc/rc.local

export JAVA_HOME=”/usr/java/latest”
```

###### Jenkins Install

- Add the Jenkins repo to your yum sources on the CentOS node

```sh
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

- Import the Jenkins rpm signing key

```sh
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

- Install the Jenkins package

```sh
yum install -y jenkins-2.19.4-1.1
```

- Check for services running on 8080 before starting the Jenkins service

```sh
netstat -tulpn | grep 8080
```

- If nothing is running on 8080, go ahead and start the service via systemctl

```sh
systemctl start jenkins
```

- Enable the Jenkins service so it starts on system startup

```sh
systemctl enable jenkins
```

- Check again for services running on port 8080

```sh
watch n=1 "netstat -tulpn | grep 8080"
```

``Ctrl-C`` to exit

- Visit the web GUI

```
http://your-server-fqdn:8080/
```

- ``initialAdminPassword``

```sh
cat /var/lib/jenkins/secrets/initialAdminPassword
```

- Paste the password into Install Wizard

- Choose ``Install Suggested Plugins``

- Set admin settings, user, password, etc.

- Press ``Enter``

- Click ``Start Using Jenkins``

- Now you have your Jenkins Master up and running!