#### 8. Adding a Jenkins Slave

```sh
sudo su -
su jenkins -s /bin/bash
ssh-keygen
```

![slave](images/8/1.png)

```sh
cat /var/lib/jenkins/.ssh/id_rsa.pub
```

![slave](images/8/2.png)

```sh
sudo su -
useradd -d /var/lib/jenkins jenkins
mkdir /var/lib/jenkins/.ssh
vi /var/lib/jenkins/.ssh/authorized_keys
```

![slave](images/8/3.png)

```sh
cd /home/user/
ls
scp jdk-8u151-linux-x64.rpm user@54.210.227.67:~/
```

![slave](images/8/4.png)

```sh
cd /home/user/
ls
rpm -Uvh jdk-8u151-linux-x64.rpm
```

![slave](images/8/5.png)

```sh
alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000
alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000
```

![slave](images/8/6.png)

```
export JAVA_HOME="/usr/java/latest"
```

![slave](images/8/7.png)

![slave](images/8/8.png)

![slave](images/8/9.png)

![slave](images/8/10.png)

![slave](images/8/11.png)

![slave](images/8/12.png)

![slave](images/8/13.png)

![slave](images/8/14.png)

![slave](images/8/15.png)

![slave](images/8/16.png)

![slave](images/8/17.png)

![slave](images/8/18.png)

![slave](images/8/19.png)

![slave](images/8/20.png)

![slave](images/8/21.png)

![slave](images/8/22.png)

![slave](images/8/23.png)

![slave](images/8/24.png)

![slave](images/8/25.png)

![slave](images/8/26.png)

![slave](images/8/27.png)