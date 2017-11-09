#### 28. Configuring and Running a Pipeline

```sh
ls
cd java-project/
ls
vi Jenkinsfile
```

```
pipeline {
  agent any

  stages {
     stage('build') {
	sh 'ant -f build.xml -v'
     }
  }
}
```

![pipe](images/28/1.png)

```sh
git status
git add .
git commit -m "setting up jenkins file"
git push origin development
```

![pipe](images/28/2.png)

![pipe](images/28/3.png)

![pipe](images/28/4.png)

![pipe](images/28/5.png)

![pipe](images/28/6.png)

![pipe](images/28/7.png)

![pipe](images/28/8.png)

![pipe](images/28/9.png)

![pipe](images/28/10.png)

![pipe](images/28/11.png)

![pipe](images/28/12.png)

![pipe](images/28/13.png)

![pipe](images/28/14.png)

![pipe](images/28/15.png)

```
pipeline {
  agent any

  stages {
     stage('build') {
		 steps {
	   		sh 'ant -f build.xml -v'
		 }
     }
  }
}
```

![pipe](images/28/16.png)

![pipe](images/28/17.png)

![pipe](images/28/18.png)

![pipe](images/28/19.png)