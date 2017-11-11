#### 43. The Jenkins CLI

```sh
sudo su -
ssh-keygen
cat .ssh/id_rsa.pub
```

![](images/43/1.png)

![](images/43/2.png)

![](images/43/3.png)

![](images/43/4.png)

![](images/43/5.png)

```sh
wget -P /var/lib/jenkins http://localhost:8080/jnlpJars/jenkins-cli.jar
```

![](images/43/6.png)

```sh
ls -la /var/lib/jenkins | grep jar
```

![](images/43/7.png)

```sh
echo "JENKINS_URL='http://localhost:8080'" >> /etc/environment
cat /etc/environment
echo "alias jenkins-cli='java -jar /var/lib/jenkins/jenkins-cli.jar'" >> ~/.bashrc
source ~/.bashrc
jenkins-cli
```

![](images/43/8.png)

```sh
jenkins-cli -s http://localhost:8080
```

![](images/43/9.png)

```sh
jenkins-cli -s http://localhost:8080 who-am-i
jenkins-cli -s http://localhost:8080 build "Freestyles/MyFreeStyleProject"
jenkins-cli -s http://localhost:8080 version
jenkins-cli -s http://localhost:8080 shutdown
jenkins-cli -s http://localhost:8080 safe-shutdown
```

![](images/43/10.png)

![](images/43/11.png)

![](images/43/12.png)

![](images/43/13.png)

![](images/43/14.png)

```sh
jenkins-cli -s http://localhost:8080 install-plugin thinBackup -restart
```

![](images/43/15.png)

![](images/43/16.png)

![](images/43/17.png)

```sh
jenkins-cli -s http://localhost:8080 console "Freestyle/MyFreestyleProject" 51
```