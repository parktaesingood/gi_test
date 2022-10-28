# git advanced

## 0. 사전준비

1. 깃허브에 원격 repository 생성
2. git clone을 통해 local repositoryfh qhrtk

## 1. 복습

1. untracked
    - git은 파일 관리를 총 2가지로 구분
    - 윈도우 기준으로 폴더 내부에 '.git'폴더가 조재하면 자동으로 추적된다
    -'.gitignore' 사용을 통해 폴더나 파일을 untracked상태로 만들 수 있다.

2. tracked
    - git이 변화를 감지하고 있는 상태
    - tracked 상태는 아래 3가지로 나눌 수 있다
        - unmodified
            - 수정하지 않은 파일 (== 최신파일)
            - local git에 올라간 파일과 비교하였을 때 수정되지 않은 상태
        - modified (vscode : changes)
            - 수정된 파일
        - staged (vscode : staged changes)
            - commit 하기 위해 기다리는 상태
            - 이 영역을 __staging Area__ 라고 부른다

> 명령어 정리 : local git repository
```
현재 디렉토리를 git 작업 디렉토리로 초기화 : git init

unmodified  ->  modified : 파일을 수정

modified  ->  staged  : git add

staged  -> local repository : git commit

현재 git 파일들 상태 확인  : git status

내 작업 내역 확인 : git log
    - commit id, 작성자, 날짜, commit message 확인 가능
    - 종료 명령어 : q
```


> 명령어 정리 : Remote Git Repository
```
1. 최초 작업시
Local Repo  -> Remote Repo       : git remote add
Remote Repo   -> Local Repo      : git clone



2. 진행 중일 때 
Local Repo  -> Remote Repo       : git push
Remote Repo   -> Local Repo      : git pull

```

## git restore

- 워킹 디렉토리에서 수정한 파일을 수정 전(직전 커밋으로) 되돌리기
- 이미 버전 관리가 되고 있는 파일만 되돌리기 가능
- git restore 통해 되돌리면 해당 내용을 복원할 수 없다
- git restore {파일 이름}
- git checkout --{파일 이름}  git 2.23.0버전 이전

## 2. 작업 단계 되돌리기 (작업 취소)

취소는 크게 2가지로 나뉜다

### 1. 직전 작업 취소

#### Working Directory 작업 취소
    - Modified 상태의 파일을 직전 commit으로 되돌림
    - 'git restore <파일명>`
    - 이미 버전 관리가 되고 있는 파일만 되돌리기 가능
    - 되돌린 내용은 복원할 수 없으니 주의해야 함

#### staging Area 작업 취소
    - Staged 상태의 파일을 Modified 상태로 되돌림 (add취소)
    - root-commit 여부에 따라 두가지로 나뉨
        - root-commit : 이전에 commit을 한 적이 있는 파일이면 True
        - root-commit이 없는 경우 : 'git rm --cached <파일명>'
        - root-commit이 있는 경우 : `git restore --staged <파일명>`

#### repository 작업 취소
    - commit을 완료한 파일을 stagint Area로 되돌리기 (commit 취소)
    - 명령어 : `git commit --amend`
    - Staging Area에 다른 파일이 올라와 있는가에 다라서 두가지로 나뉨
        - Staging Area에 새로 올라온 내용이 없다면 : 직전commit의 메시지만 수정
        - Stanging Area에 새로 올라온 내용이 있다면 : 직전 commit을 새로운 commmit으로 덮어쓰기
        - 이 때 Staging Area의 모든 내용이 commit에 포함된다
    - commit 메시지 수정을 위해 vim 편집기가 열린다
        - 입력 모드(i) : 문서 편집 가능
        - 명령 모드(esc)
            - 명령 모드는 `:`와 함께 사용한다
            - 저장 후 종료 (:wq)
            - 강제 종류 (:q!)
                - 리눅스에서 특정 동작을 강제로 수행하게 하는 것 `!`

 
### 2. 과거 작업으로 돌아가기

    - git reset의 세가지 옵션
        --soft : 해당 커밋으로 되돌아가고 되돌아간 커밋 이후의 파일들은 Staging Area로 돌려놓음
        --mized : 해당 커밋으로 되돌아가고 되돌아간 커밋 이후의 파일들은 working Directory로 돌려놓음
        --hard : 되돌아간 커밋 이후의 파일들은 모두 working Directory에서 삭제  -> 사용시 주의!!! 왠만하면 안써
        

