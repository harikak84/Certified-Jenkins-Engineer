#### 15. Git Hooks and Other Build Triggers

![git](images/15/1.png)

![git](images/15/2.png)

![git](images/15/3.png)

![git](images/15/4.png)

![git](images/15/5.png)

![git](images/15/6.png)

![git](images/15/7.png)

![git](images/15/8.png)

- Using ``Git plugin``

![git](images/15/9.png)

![git](images/15/10.png)

![git](images/15/11.png)

![git](images/15/12.png)

![git](images/15/13.png)

![git](images/15/14.png)

```sh
ls
cd jenkins-test/
ls
touch newfile.txt
git status
git add .
git commit -am "testing git webhook"
git push origin master
```

![git](images/15/15.png)

![git](images/15/16.png)

![git](images/15/17.png)

![git](images/15/18.png)

- Using ``GitHub plugin``

![git](images/15/19.png)

![git](images/15/20.png)

![git](images/15/21.png)

![git](images/15/22.png)

![git](images/15/23.png)

![git](images/15/24.png)

```sh
echo "sample text" >> newfile.txt
git add .
git commit -am "testing github webhook"
git push origin master
```

![git](images/15/25.png)

![git](images/15/26.png)

![git](images/15/27.png)

![git](images/15/28.png)
