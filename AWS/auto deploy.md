## 배포 자동화

- war 배포 자동화를 해보자
- touch build.sh 혹은 vi build.sh 로 쉘 스크립트 파일 생성한다.
- chmod +x build.sh 로 해당 파일에 실행권한을 부여한다.
- ./build.sh 로 해당 파일을 실행 할 수 있다.


### STEP1 

- 평소 배포 시 진행하던 순서로 쉘 스크립트로 작성하였다.

```shell
############################### directory root ##########################
#
# ~/github/apache-tomcat-9.0.34/webapps
# ~/github/apache-tomcat-9.0.34/bin
# ~/github/sidedish-11/BE/sidedish11/build/libs
#
#########################################################################
#!/bin/bash
echo "hello! build start!"

# tomcat shutdown
~/github/apache-tomcat-9.0.34/bin/shutdown.sh

# delete .war
rm -rf ~/github/apache-tomcat-9.0.34/webapps/ROOT.war

# git pull
cd ~/github/sidedish-11
git pull

# build
cd ~/github/sidedish-11/BE/sidedish11/
./gradlew bootWar -x test

cd ~/github

# copy .war to tomcat directory
cp ~/github/sidedish-11/BE/sidedish11/build/libs/ROOT.war ~/github/apache-tomcat-9.0.34/webapps

# tomcat startup
~/github/apache-tomcat-9.0.34/bin/startup.sh

echo "done!"
```



### STEP2

- head가 가리키는 커밋을 비교하여 변경되었을때와 그렇지 않을 때를 비교한다.
- `와 '는 다르니 꼭 주의하자.

```shell
#!/bin/bash

cd ~/github/sidedish-11

git fetch

# ` and ' not same, careful
now=`git rev-parse HEAD`
origin=`git rev-parse origin/dev`

if [ $now == $origin ]; then
        echo "nothing to do"
        echo "now -> ${now}"
        echo "origin -> ${origin}"
else
        echo "changed"
        echo "now -> ${now}"
        echo "origin -> ${origin}"
fi
```



### STEP3

- step1과 step2를 합쳐 변경사항이 있는 경우에만 빌드하여 배포한다.
- war deploy

```shell
############################### directory root ##########################
#
# ~/github/apache-tomcat-9.0.34/webapps
# ~/github/apache-tomcat-9.0.34/bin
# ~/github/sidedish-11/BE/sidedish11/build/libs
#
#########################################################################

#!/bin/bash
echo "hello! checking any updates..."

# move to directory
cd ~/github/sidedish-11
git fetch

# ` and ' not same, careful
now=`git rev-parse HEAD`
origin=`git rev-parse origin/dev`

if [ $now == $origin ]; then
        echo "nothing changed"
        echo "now -> ${now}"
        echo "origin -> ${origin}"
else
        echo "changed"
        echo "now -> ${now}"
        echo "origin -> ${origin}"
        echo "build start!!!"

        # tomcat shutdown
        ~/github/apache-tomcat-9.0.34/bin/shutdown.sh

        # delete .war
        rm -rf ~/github/apache-tomcat-9.0.34/webapps/ROOT.war

        # git pull
        cd ~/github/sidedish-11
        git pull

        # build
        cd ~/github/sidedish-11/BE/sidedish11/
        ./gradlew bootWar -x test

        cd ~/github

        # copy .war to tomcat directory
        cp ~/github/sidedish-11/BE/sidedish11/build/libs/ROOT.war ~/github/apache-tomcat-9.0.34/webapps

        # tomcat startup
        ~/github/apache-tomcat-9.0.34/bin/startup.sh

        echo "done"
fi
```

- jar deploy


```shell
############################### directory root ##########################
#
# ~/github/issue-tracker-12
#
#########################################################################

#!/bin/bash
echo "hello! checking any updates..."

# move to directory
cd ~/github/issue-tracker-12
git fetch

# ` and ' not same, careful
now=`git rev-parse HEAD`
origin=`git rev-parse origin/dev`

if [ $now == $origin ]; then
        echo "nothing changed"
        echo "now -> ${now}"
        echo "origin -> ${origin}"
else
        echo "changed"
        echo "now -> ${now}"
        echo "origin -> ${origin}"
        echo "build start!!!"

        # jar shutdown
        kill $(lsof -t -i:8080)

        # git pull
        cd ~/github/issue-tracker-12
        git pull

        # build
        cd ~/github/issue-tracker-12/BE/issue-tracker
        ./gradlew build -x test

        # jar startup
        cd ~/github/issue-tracker-12/BE/issue-tracker/build/libs
        nohup java -jar issue-tracker-0.0.1-SNAPSHOT.jar &

        echo "done"
fi
```


### STEP4

- Crontab을 이용하여 일정 시간마다 dev 브랜치에 업데이트 사항이 있을 경우에만 업데이트 한다.

```shell
# open crontab vi
crontab -e 

# show operating crontab
crontab -l

# delete all crontab
crontab -r
```



