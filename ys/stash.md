# stash 
- 코드를 수정하는 도중 다른 브랜치에서 작업해야할 일이 생겼을때 임시로 수정된 코드를 저장하는 기능  
- 현재 워킹 디렉토리의 내역을 별도 스택 영역에 잠시 보관

## stash 저장
```sh
$ git init 
$ vi stash.txt
$ git add stash.txt

// default name 으로 stash 생성
$ git stash 
// stash 이름 지정 가능
$ git status save "WIP: someController 수정 중"

$ git stash list
$ git checkout -b feature-1
```
### stash 를 사용하지 않는 방법
```
$ git commit -am "temp"
# ------
# 다른 브랜치에서 작업 
# 현재 브랜치로 다시 돌아와서
# ------
$ git reset -soft HEAD^
```

### stash 저장 범위
stash 는 기본적으로 tracked 상태의 파일만 저장  
untracked 상태의 파일을 같이 저장하려면 `--include-untracked` or `-u` 옵션 사용

## stash 확인
- stash 의 저장 영역은 stack (FILO)
```sh
$ git stash list

# git은 스태시된 객체들을 .git/refs/stash 에 저장
```
- 변경 내용 확인
```
$ git stash show

# 특정 스태시 확인
$ git stash show -p stash0{2}
```

## stash 불러오기
```
git stash pop
```
- 가장 마지막 stash 를 불러오고 불러온 스태시는 삭제됨  
- 스태시를 불러올때 워킹 디렉터리와 자동으로 병합됨

### 참고사항 
stash 는 저장할때는 워킹디렉토리와 스테이지 영역의 파일까지 저장하지만 복원시엔 워킹 디렉토리만 돌려놓음  
=> add 된 파일을 stash 하더라도 pop 시엔 add 가 안된 상태로 복원  
=> 만약 add 된 상태 그대로 가져오려면 `git stash pop --index`

### stash 복사
stash pop 사용 시 stash 가 스택에서 삭제됨  
삭제하지 않으려면  `git stash apply`   
특정 stash 를 가져오려면 `git stash apply {stash 명}`

### stash 삭제
```
$ git stash drop
$ git stash drop {stash 명}
```

# clean
개발 과정 생성된 임시 파일들(untracked file)을 정리할 수 있음  
```sh
# git clean

# 단, 바로 clean 시 삭제 안됨 
# 옵션을 추가해줘야함
-f : 강제로 clean 
-n : clean 사용 전 가상으로 미리 실행해보기
-d : 추적되지 않는 파일만 삭제 (-f 옵션이랑 같은거같은데..)
-x : clean 기본 동작은 .gitignore 에 등록된 파일은 삭제 x, .gitignore 에 등록된 파일도 같이 삭제 하고싶을 떄 사용
```





