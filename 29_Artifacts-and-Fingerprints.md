#### 29. Artifacts and Fingerprints

- ``Jenkinsfile``

```
pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
  }

  stages {
     stage('build') {
	steps {
	   sh 'ant -f build.xml -v'
	}
     }
  }

  post {
    always {
      archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
    }
  }
}
```

![af](images/29/1.png)

```sh
git add .
git commit -am "setting up archive for jar file"
git push origin development
```

![af](images/29/2.png)

![af](images/29/3.png)

![af](images/29/4.png)

![af](images/29/5.png)

![af](images/29/6.png)

![af](images/29/7.png)

![af](images/29/8.png)

![af](images/29/9.png)

![af](images/29/10.png)

![af](images/29/11.png)

![af](images/29/12.png)

![af](images/29/13.png)

![af](images/29/14.png)

![af](images/29/15.png)

![af](images/29/16.png)

![af](images/29/17.png)

![af](images/29/18.png)

```sh
cd /var/lib/jenkins/
ls
cd jobs/
ls
cd MyJavaProject/
ls
cd builds/
ls
cd 6/
ls
cd archive/
ls
cd dist/
ls
md5sum rectangle_\$\{env.MAJOR_VERSION\}.6.jar
```

![af](images/29/19.png)

![af](images/29/20.png)

![af](images/29/21.png)

![af](images/29/22.png)

![af](images/29/23.png)

![af](images/29/24.png)

![af](images/29/25.png)

![af](images/29/26.png)

![af](images/29/27.png)

![af](images/29/28.png)

![af](images/29/29.png)

![af](images/29/30.png)

![af](images/29/31.png)

![af](images/29/32.png)

![af](images/29/33.png)

![af](images/29/34.png)

![af](images/29/35.png)

![af](images/29/36.png)

![af](images/29/37.png)

![af](images/29/38.png)

![af](images/29/39.png)

![af](images/29/40.png)

![af](images/29/41.png)

![af](images/29/42.png)

![af](images/29/43.png)

![af](images/29/44.png)

![af](images/29/45.png)

![af](images/29/46.png)

![af](images/29/47.png)

![af](images/29/48.png)

![af](images/29/49.png)
