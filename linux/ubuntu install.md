## 리눅스(ubuntu) 설치 가이드

1. 듀얼부팅 설치 가이드

   https://cupjoo.tistory.com/53

2. Grub 못잡는 에러

   - 윈도우에서 직접 부트 순서를 정해준다. 관리자 권한으로 터미널 실행 후 아래 명령어 입력한다.

     ```
     bcdedit /set {bootmgr} path \EFI\ubuntu\shimx64.efi
     ```

3. 무한 로그인 에러

   https://mesnotes.tistory.com/12
