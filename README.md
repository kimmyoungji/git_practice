# KMJ

## git 명령어
- ```git init``` .git 폴더 생성
---
- ```git add <target-file-path or .>``` 작업 폴더 내의 변경 사항을 Staging area에 올리기
- ```git commit -m "commit msg"``` Staging area에 등록된 변경사항을 로컬레포에 반영하기
---
- ```git stash``` 작업 폴더 내의 변경 사항을 Staging area에 올리거나, commit하지 않고 임시적으로 다른 공간에 저장하는 것
- ```git stash pop``` 가장 최근 stash한 변경 사항을 다시 작업 폴더에 반영하기 
- ```git stash apply``` stash한 변경사항을 stash 스택에서 제거하지 않고, 해당 변경 사항을 작업 폴더에 반영하기
- ```gut stash list``` stash한 내역 출력
- ```git stash apply stash@{1}``` 특정 stash 내역을 지정하여 apply
---
- ```git log``` 커밋 내역 보기
- ```git revert <commit-hash>``` 특정 커밋 내역을 취소하는 커밋 만들기
- ```git revert -m 1 <merge-commit-hash>``` 머지 커밋 내역을 취소하는 커밋 만들기 '-m 1'은 어느 부모의 커밋 내역을 결정(?)

---
- ```git reset``` 깃 레포의 변경사항을 취소하기. staging 취소, 커밋 취소. 
- ```git reset .``` 현재 Staging area의 모든 변경사항을 Staging area에서 내리기
- ```git reset --soft HEAD~1``` 
  -  '--soft' 는 커밋까지만 취소, Staging area에는 변경사항이 유지된다.
  -  'HEAD' 는 현재 브랜치의 가장 최신 커밋
  -  'HEAD\~1' 은 가장 최신 커밋 1개 취소하기. 'HEAD\~2'일 경우 가장 최신 커밋 2개 취소하기. 'HEAD\~3'이면 가장 최신 커밋 3개 취소하기 ...
  -  'HEAD^1' 은 merge commit에 대해 주로 사용. 첫번째 부모브랜치(merge시, 현재브랜치였던 브랜치)의 마지막 커밋으로 되돌리기. 
  -  'HEAD^2' 은 merge commit에 대해 주로 사용. 두번째 부모브랜치(merge시, 현재브랜치가 아니였던 브랜치)의 마지막 커밋으로 되돌리기. 
- ```git reset --mixed HEAD~1``` 
  -  '--mixed' 는 Staging area까지만 취소, working directory에는 변경사항이 유지된다.
- ```git reset --hard HEAD~1```
  -  '--hard' 는 working directory의 변경사항까지 모두 취소한다. (사용주의)
---
- ```git restore <file-path or .>``` 커밋되지 않은 변경사항을 모두 취소하고 최신 커밋 시점으로 되돌리기
---
- ```git rebase``` 브랜치의 베이스 커밋을 재설정하기
  - rebase시 커밋들이 새로운 커밋 해쉬값을 할당받게 된다. 이는 동일한 변경 내용이지만 해쉬값이 다른 커밋을 만들어내 깃 레포지토리 작업에 혼란을 줄 수 있기 때문에 주의해야한다 자세한 내용은 (https://velog.io/@alsry922/rebase%EC%99%80-merge)
---
- ```git branch <new-branch-name>``` 새로운 로컬브랜치 만들기
- ```git checkout <local-branch-name>``` 작업 브랜치 변경하기
- ```git checkout -b <new-branch-name>``` 새로운 로컬브랜치 만들고 작업 브랜치 변경하기
---
- ```git clone <repo_http_or_ssh_url> .``` 원격 깃 레포지토리 연결 및 복제
- ```git remote add origin <repo_url>```  원격 깃 레포지토리 추가
- ```git remote -v``` 원격 깃 레포지토리 나열
---
- ```git pull``` 로컬브랜치에 원격브랜치 내용 반영하기
  - 현재브랜치의 이름과 동일한 원격브랜치와 연결되어 있을 때만 이렇게 사용할 수 있다. 예를 들어 현재브랜치가 test1 이라고 했을 때, 연결된 원격레포/브랜치가 origin/test1 이어야만 한다. 그렇지 않을 경우 아래와 같이 명시해주어야 한다. 아래 push도 마찬가지이다.
- ```git push``` 원격브랜치에 로컬브랜치 내용 반영하기
  - git push 결과 해석
  ```bash
  $ git push origin main
  Enter passphrase for key '/Users/username/.ssh/id_ed25519': 
  Counting objects: 5, done.  # 5개의 오브젝트 세었음
  Delta compression using up to 8 threads. # 델타 압축 수행시 최대 8개의 스레드를 사용하여 병렬처리를 수행한다.
  Compressing objects: 100% (3/3), done.   # 3개의 객체를 압축하고 완료했음, 모든 객체가 성공적으로 압축되었음.
  Writing objects: 100% (3/3), 380 bytes | 380.00 KiB/s, done. # 3개의 객체를 원격 저장소에 쓰는 작업이 완료되었음. 데이터 크기는 389바이트이며 전송적도는 380.00 KiB/s이다.
  Total 3 (delta 1), reused 0 (delta 0) # 총 3개의 객체가 전송되었으며, 그 중 1개는 델타 업축을 사용하였음. 재사용된 객체는 없다.
  To git@github.com:user/repo.git
    abc1234..def5678  main -> main # 로컬레포의 변경사항을 원격레포에 성공적으로 푸시했음. 

  # 푸쉬 과정: 객체 수 계산, 델타 압축 수행, 객체 압축 및 전송, 원격 브랜치의 업데이트
  ```
- ```git push <remote-name> <local-branch-name>``` 원격레포로 로컬브랜치 반영하기 
  - (로컬브랜치와 동일한 이름의 원격브랜치가 없을 경우, 원격브랜치에 자동생성된다.)
- ```git pull <remote-name> <local-branch-name>``` 로컬브랜치에 원격레포 변경사항 반영하기 (실제 변경 내용을 받아와 반영함)
  -  (로컬 브랜치와 동일한 이름의 원격브랜치가 없을 경우, 풀 실패)
  -  git pull = git fetch + git merge
- ```git fetch``` 원격레포의 변경사항을 받아오기 (실제 변경 내용을 받아와 반영하지 않음)
  - git fetch 결과 해석
      ```bash
      git fetch

      remote: Enumerating objects: 6, done.  # 원격레포의 6개 객체를 열거함
      remote: Counting objects: 100% (6/6), done. # 원격레포의 6개 객체를 세었음
      remote: Compressing objects: 100% (6/6), done. # 원격레포의 6개 객체를 압축함
      remote: Total 6 (delta 2), reused 0 (delta 0), pack-reused 0 # 총 6개의 기본객체가 있고 그 중에 두개의 델타객체가 있음. 재사용된 객체는 없음.   
                                                                  # 델타 객체란 기본객체와 비교했을 때의 차이점만 저장하는 객체
      ```
- ```git merge <source-local-branch>``` 현재브랜치로 소스로컬브랜치를 병합하기 
- ```git merge <remote-name>/<source-remote-branch>``` 현재브랜치로 소스원격브랜치를 병합하기 (merge 이전에 git fetch한 결과, 병합할 변경사항이 있어야함)
---
- ```git branch --set-upstream-to=<remote-name>/<remote-branch-name>  <current-branch-name>``` 원격브랜치와 로컬브랜치 연결하기
- ```git checkout -b <remote-name>/<remote-branch-name>``` 원격브랜치와 로컬브랜치 한번에 만들고 작업브랜치 변경하기
