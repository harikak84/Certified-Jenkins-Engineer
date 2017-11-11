#### 41. Hands-on Lab: Configure a Jenkins Multibranch Pipeline

- Disable ``SELinux``

```sh
sudo setenforce 0
```

![](images/41/1.png)


- Install ``Docker``

```sh
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum clean all
sudo yum install docker-ce
sudo systemctl start docker
```

![](images/41/2.png)

![](images/41/3.png)

![](images/41/4.png)

![](images/41/5.png)

- Pull the Jenkins Docker image:

```sh
sudo docker pull jenkins:2.19.4
```

![](images/41/6.png)

- Create a directory for the Jenkins container to share on the host

```sh
sudo mkdir /var/jenkins_home
```

![](images/41/7.png)

- Run the container

```sh
sudo docker run -d -u root -p 8080:8080 -p 50000:50000 -v /var/jenkins_home:/var/jenkins_home jenkins:2.19.4
```

![](images/41/8.png)

- Complete the ``jenkins`` setup

```sh
sudo cat /var/jenkins_home/secrets/initialAdminPassword
```

![](images/41/9.png)

- Setup the Project

![](images/41/10.png)

![](images/41/11.png)

![](images/41/12.png)

![](images/41/13.png)

![](images/41/14.png)

![](images/41/15.png)

![](images/41/16.png)

![](images/41/17.png)

- Generate SSH Keys for the Containerized ``Jenkins`` Master

```sh
sudo docker ps
sudo docker exec -it 810bb0d152b4 bash
cd ~
ssh-keygen
cat .ssh/id_rsa.pub
```

![](images/41/18.png)

![](images/41/19.png)

![](images/41/20.png)

![](images/41/21.png)

![](images/41/22.png)

![](images/41/23.png)

![](images/41/24.png)

- Configure and Run a Multibranch Pipeline

![](images/41/25.png)

![](images/41/26.png)

![](images/41/27.png)

![](images/41/28.png)

![](images/41/29.png)

![](images/41/30.png)

```sh
git clone https://github.com/Kan1shka9/content-jenkins-multibranch-pipeline.git
cd content-jenkins-multibranch-pipeline/
git checkout development
vi Jenkinsfile
```

```
pipeline {
    agent any stages {
        stage('build') {
            steps {
              sh 'javac -d . src/*.java' 
              sh 'echo Main-Class: Rectangulator > MANIFEST.MF' 
              sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'rectangle.jar', fingerprint: true
                }
            }
        }
        stage('run') {
            steps {
                sh 'java -jar rectangle.jar 7 9'
            }
        }
        stage('Promote Development to Master') {
            when {
                branch 'development'
            }
            steps {
                echo 'Stashing Local Changes' 
              	sh 'git stash' 
              	echo 'Checking Out Development' 
              	sh 'git checkout development' 
              	sh 'git pull origin' 
              	echo 'Checking Out Master' 
             	sh 'git checkout master' 
              	echo 'Merging Development into Master' 
              	sh 'git merge development' 
              	echo 'Git Push to Origin' 
              	sh 'git push origin master'
            }
        }
    }
}
```

![](images/41/31.png)

```sh
git commit -am "added promotion stage"
git push origin development
```

![](images/41/32.png)

- Tagging

```sh
vi Jenkinsfile
```

```
pipeline {
  agent any

  environment {
    MAJOR_VERSION = 1
  }

  stages {
    stage('build') {
      steps {
        sh 'javac -d . src/*.java'
        sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
        sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
      }
      post {
        success {
          archiveArtifacts artifacts: 'rectangle.jar', fingerprint: true
        }
      }
    }
    stage('run') {
      steps {
        sh 'java -jar rectangle.jar 7 9'
      }
    }
    stage('Promote Development to Master') {
      when {
        branch 'development'
      }
      steps {
        echo "Stashing Local Changes"
        sh "git stash"
        echo "Checking Out Development"
        sh 'git checkout development'
        sh 'git pull origin'
        echo 'Checking Out Master'
        sh 'git checkout master'
        echo "Merging Development into Master"
        sh 'git merge development'
        echo "Git Push to Origin"
        sh 'git push origin master'
      }
    }
    stage('Tagging the Release') {
      when {
        branch 'master'
      }
      steps {
        sh "git tag rectangle-${env.MAJOR_VERSION}.${BUILD_NUMBER}"
        sh "git push origin rectangle-${env.MAJOR_VERSION}.${BUILD_NUMBER}"
      }
    }
  }
}
```

```sh
git commit -am "added tagging stage"
git push origin development
```

![](images/41/33.png)

![](images/41/34.png)

![](images/41/35.png)

![](images/41/36.png)

- Notification

![](images/41/37.png)

![](images/41/38.png)

![](images/41/39.png)

![](images/41/40.png)

![](images/41/41.png)

```sh
vi Jenkinsfile
```

```
pipeline {
  agent any

  environment {
    MAJOR_VERSION = 1
  }

  stages {
    stage('build') {
      steps {
        sh 'javac -d . src/*.java'
        sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
        sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
      }
      post {
        success {
          archiveArtifacts artifacts: 'rectangle.jar', fingerprint: true
        }
      }
    }
    stage('run') {
      steps {
        sh 'java -jar rectangle.jar 7 9'
      }
    }
    stage('Promote Development to Master') {
      when {
        branch 'development'
      }
      steps {
        echo "Stashing Local Changes"
        sh "git stash"
        echo "Checking Out Development"
        sh 'git checkout development'
        sh 'git pull origin'
        echo 'Checking Out Master'
        sh 'git checkout master'
        echo "Merging Development into Master"
        sh 'git merge development'
        echo "Git Push to Origin"
        sh 'git push origin master'
      }
      post {
        success {
          emailext(
            subject: "${env.JOB_NAME} [${env.BUILD_NUMBER}] Development Promoted to Master",
            body: """<p>'${env.JOB_NAME} [${env.BUILD_NUMBER}]' Development Promoted to Master":</p>
            <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
            to: "brandon@linuxacademy.com"
          )
        }
      }
    }
    stage('Tagging the Release') {
      when {
        branch 'master'
      }
      steps {
        sh "git tag rectangle-${env.MAJOR_VERSION}.${BUILD_NUMBER}"
        sh "git push origin rectangle-${env.MAJOR_VERSION}.${BUILD_NUMBER}"
      }
      post {
        success {
          emailext(
            subject: "${env.JOB_NAME} [${env.BUILD_NUMBER}] NEW RELEASE",
            body: """<p>'${env.JOB_NAME} [${env.BUILD_NUMBER}]' NEW RELEASE":</p>
            <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
            to: "brandon@linuxacademy.com"
          )
        }
      }
    }
  }
}
```

```sh
git commit -am "adding notifications"
git push origin development
```

![](images/41/42.png)

![](images/41/43.png)

![](images/41/44.png)

![](images/41/45.png)

![](images/41/46.png)

![](images/41/47.png)