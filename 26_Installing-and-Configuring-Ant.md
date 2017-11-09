#### 26. Installing and Configuring Ant

[``Ant binary``](http://ant.apache.org/bindownload.cgi)

```sh
wget http://apache.spinellicreations.com//ant/binaries/apache-ant-1.10.1-bin.tar.gz
tar xvzf apache-ant-1.10.1-bin.tar.gz -C /opt
```

![ant](images/26/1.png)

![ant](images/26/2.png)

```sh
ln -s /opt/apache-ant-1.10.1/ /opt/ant
sh -c 'echo ANT_HOME=/opt/ant >> /etc/environment'
ln -s /opt/ant/bin/ant /usr/bin/ant
```

![ant](images/26/3.png)

```sh
ln -s /opt/apache-ant-1.10.1/ /opt/ant
ln -s /opt/ant/bin/ant /usr/bin/ant
```

![ant](images/26/4.png)

```sh
ant -version
```

![ant](images/26/5.png)

![ant](images/26/6.png)

```sh
cd java-project/
touch build.xml
vi build.xml
```

![ant](images/26/7.png)

```sh
git status
git add .
git commit -m "added build.xml"
git push origin development
```

![ant](images/26/8.png)

```sh
su jenkins -s /bin/bash
pwd
cd /var/lib/jenkins/
```

![ant](images/26/9.png)

```sh
git clone https://github.com/Kan1shka9/java-project.git
cd java-project/
ls
git checkout development
ls
```

![ant](images/26/10.png)

```sh
ant -f build.xml -v
```

![ant](images/26/11.png)

```sh
ls
cd dist/
ls
java -jar rectangle_\$\{env.MAJOR_VERSION\}.\$\{env.BUILD_NUMBER\}.jar 4 5
```

![ant](images/26/12.png)

```sh
cd ../../
rm -rf java-project/
```

![ant](images/26/13.png)