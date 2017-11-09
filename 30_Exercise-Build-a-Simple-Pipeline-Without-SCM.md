#### 30. Exercise: Build a Simple Pipeline Without SCM

```sh
pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('PRINT') {
            steps {
                sh 'echo $JOB_NAME'
            }
        }
        stage('WRITE') {
            steps {
                sh 'echo $BUILD_NUMBER >> build_number'
            }
        }
        stage('READ') {
            steps {
                sh 'cat build_number'
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'build_number', fingerprint: true
        }
    }
}
```

![pipe](images/30/1.png)

![pipe](images/30/2.png)

![pipe](images/30/3.png)

![pipe](images/30/4.png)

![pipe](images/30/5.png)

![pipe](images/30/6.png)

![pipe](images/30/7.png)

![pipe](images/30/8.png)

![pipe](images/30/9.png)

