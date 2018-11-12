# Git과 SSH Key 인증 방식 Know-how

## SSH Key 변경 이후 인증에 문제가 있을 경우

### 인증 문제여부 확인방법
- git pull
- git fetch
- 위의 명령어를 실행하면 인증이 안되는 경우가 있음.

### 해결 방법
- Git 저장소의 Remote URL을 갱신해주면 해결 된다.

``` bash
> git remote set-url origin git@github.com:{ user }/{ repository_name }.git
```
