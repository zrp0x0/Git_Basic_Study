# Git / Github

## git 설치법 (윈도우)

### git이란?
- 버전관리 소프트웨어
- 작업한 코드를 기록, 보관 기능
- 과거로 이전 가능
- 과거 작업 내용 열람 가능

### git install
- git download window 버전 설치
- 설치 시 설정 사항 (Optional / Recommand)
    - Use Visual Studio Code as Git's default editor
        - VSC를 git 기본 에디터로 설정

    - Override the default branch name for new repositories - main
        - 새로운 저장소 브랜치 이름을 기본으로 main으로 설정 -> 나중에 github 연동 시 좋음

### git 최초 설정
- 아무 폴더나 만들고 shift + 우클릭
- powershell 열기
```bash
git --version # git이 잘 설치되었는지 확인
git config --global user.email "내가 사용할 이메일"
git config --global user.name "내가 사용할 이름"
```
    - --global: 내 컴퓨터에 전역으로 이 설정을 적용한다는 의미
    - user.email: 내가 사용할 이메일
    - user.name: 내가 사용할 이름

---

## git add, commit으로 파일 기록

### 코드 짜면서 git 사용해보기
- 작업 폴더에서 git을 사용하고 싶으면 git init부터 입력
```bash
git init
```
    - git이라는 소프트웨어가 해당 작업 폴더를 감사, 추적하기 시작함

- 폴더를 하나 만들고 app.py라는 파일을 생성
```python
print("Hello World")
```

- 이제 이 파일에 대해서 기록을 남기로 싶다면?
```bash
git add app.py
git commit -m "create app.py"
```
    - git add <파일명>
    - git commit -m "내가 무엇을 했는지 작성"

- 만약에 해당 파일에 코드를 더 작성했다면?
```python
print("Hello World")
print("update app.py")
```

```bash
git add app.py
git commit -m "update app.py"
```

### staging이라는 용어
- 왜 굳이 2개를 입력해야하는 것일까? (add / commit)
    - 모든 파일 굳이 다 기록할 필요가 없음
    - git add라는 명령어를 통해 내가 기록할 파일부터 고르고
    - git commit이라는 명령어로 실제 기록을 
    
- 지금까지의 흐름
    - 작업 폴더 <-git add-> [ staging area ] <-git commit-> [ repository(저장소) ]

- staging
    - commit할 파일을 골랐다는 뜻

### 유용한 명령어
- git add & commit을 동시에 해주는 명령어도 있음
```bash
git commit -am "메세지"
```
    - 수정된 파일을 한 번에 스테이징 후 한 번에 커밋
    - 주의사항
        - 신규로 생성된 파일(git이 추적하지 못함)은 안됨
        ```bash
        git add . # 해당 폴더의 전체 파일 추가 (물론 gitignore 목록은 포함이 안됨)
        git commit -m "메세지"
        ```

- 만약 여러 개의 파일을 스테이징하고 싶다면?
```bash
git add app.py test_controller.py # 특정 두개 파일 스테이징
git add . # 전체 파일 스테이징
```

- 상태창 열기
```bash
git status
```
    - 어떤 파일을 스테이징 했는지
    - 어떤 파일을 수정했는지
    - 등 현재 상태를 볼 수 있음

- 내가 커밋한 내역을 보고 싶다면?
```bash
git log --all oneline
```

---

## git add, commit, diff 쉽게 하는 법 (VSCode)

### git commit 뭐하러 입력함?
- VSCode에서 GUI로 git add, commit 쉽게 가능
    - Changes 항목에서 +를 눌러서 스테이징할 수 있음 (git add)
    - Staged Changes에서 -를 눌러서 스테이징을 해제 할 수 있음 (???)
    - Commit을 누르기 전에 위에 메세지를 입력해야함 (안 하면 하라고 뜨는데 귀찮음) (git commi -m)

### git diff
- commit을 그냥 막하면 안 좋음
- commit하기 전에 이전 commit과의 파일 차이점을 확인하는 것이 좋음
```bash
git diff
```
    - 이전 commit과의 어떤 파일에서 어떤 차이가 있는지 확인할 수 있음
    - j/k로 스크롤바 조작
    - q로 종료
    - 참고할 점: 엔터키 입력도 파일의 수정으로 입력함 (그러니깐 아무것도 안하고 옆에 엔터를 눌러도 diff로 인식함)   
        - 그냥 모든 행위를 차이점으로 인식함

- 만약 좀 더 고급지게 확인하고 싶다면?
```bash
git difftool
```
    - vim editor가 뜸
    - 여기서 차이점을 분석할 수 있음
    - vim 사용법과 동일

- 조금 더 유용한 기능
```bash
git difftool <커밋아이디>
git difftool <커밋아이디1> <커밋아이디2>
```
    - 현재 파일 vs 특정 커밋 비교 가능
    - 커밋아이디1 vs 커밋아이디2 비교 가능

- 커밋 아이디란?
```bash
git log --oneline --all
# 0404cbd (HEAD -> main) update app.py add study git diff 2
# b521fb0 update app.py delete update app.py add study git diff
```
    - 여기서 맨 앞에 b521fb0같이 16진수로 나오는 이상한 숫자가 바로 커밋 아이디

### 에디터 부가기능
- 에디터에서 설치할 수 있는 VSCode의 경우 Extension을 설치해서 좋은 툴을 사용하는게 더 좋을 수도 있음
    - git graph 
    
---

## git의 branch 만들기

### branch 만드는 법

