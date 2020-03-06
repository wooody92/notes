### 1.heroku 배포

1. 배포 할 local directory 이동

2. heroku 로그인

   ```
   heroku login
   ```

3. heroku 저장소(app) 생성 (wooody92는 저장소 이름이자 도메인 이름)

   ```
   heroku create wooody92
   ```

4. heroku remote 저장소(app) local과 연결

   ```
    heroku git:remote -a wooody92
   ```

5. commit 파일 remote에 push (step1은 특정 브랜치)

   ```
   git push heroku step1:master
   
   * heroku push는 master branch로 해야한다
   * git push heroku master
   ```

> 참고 링크
>
> https://victorydntmd.tistory.com/112

-------
### 2.heroku 자동으로 ping 보내기(heroku 서버항상 open)

```
https://kaffeine.herokuapp.com
```
