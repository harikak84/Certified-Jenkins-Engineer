#### 40. Exercise: Configure Notifications in a Pipeline

```
pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Greeting') {
            steps {
                sh 'echo "Notification Time!"'
            }
        }
    }
    post {
        success {
            emailext(
                subject: "${env.JOB_NAME} [${env.BUILD_NUMBER}] Ran!",
                body: """
'${env.JOB_NAME} [${env.BUILD_NUMBER}]' Ran!": Check console output at ${env.JOB_NAME} [${env.BUILD_NUMBER}]/a> """, to: "your@email.com" ) } } }
```

![test](images/40/1.png)

![test](images/40/2.png)

![test](images/40/3.png)

![test](images/40/4.png)

![test](images/40/5.png)

![test](images/40/6.png)

![test](images/40/7.png)

![test](images/40/8.png)

![test](images/40/9.png)

![test](images/40/10.png)

![test](images/40/11.png)