<br>

# 협업 방식

<br>

## 👩‍👧‍👦Feature Branch Workflow

기능별 브랜치를 만들어 작업하는 방식으로 Feature branch에서 기능 개발이 완료되면 Master branch에서 Feature branch를 Merge하는 방식으로 Workflow가 진행된다.

다수의 팀 구성원이 master 브랜치를 중심으로 안전하게 새로운 기능을 개발할 수 있다. 

소규모 인원의 프로젝트에서 주로 사용하는 협업 방식으로 유연성이 큰 협업 방법이다. 

**장점**

- 다수의 팀원이 메인 코드 베이스(master)를 중심으로, 안전하게 새로운 기능을 개발할 수 있다.
- 중간에 브랜치를 하나 거쳐가기 때문에 Master branch는 비교적 검증된 형상을 유지할 수 있다.
- Pull request를 적용하기 쉽다.

**단점**

- 제품 개발 단계에서는 좋으나, 제품 런칭 이후 관리가 어렵게 된다.

---

<br>

## 👩‍👧‍👦Gitflow Workflow

Feature Branch Workflow보다 복잡하지만, 대형 프로젝트에 적용 할 수 있는 좀 더 엄격한 작업 절차를 가짐.

가장 큰 핵심은 중앙 원격 저장소에서 master와 develop, 두 개의 메인 브랜치 를 이용한다는 것.

- master branch: 릴리스 이력을 관리하기 위해 사용. 즉, 배포 가능한 상태만을 관리한다.
- develop branch: 기능 개발을 위한 브랜치들을 병합하기 위해 사용.(모든 기능이 추가되고 버그가 수정되어 배포 가능한 상태라면 ‘master’ 브랜치에 merge 한다.) 평소에는 이 브랜치를 기반으로 개발을 진행한다.

**장점**

- Feature branch의 장점을 모두 가지고 있다.
- 제품 런칭 이후 관리가 용이하다.
- 코드 배포를 중심으로 좀 더 엄격한 개발이 가능하다.
- 프로젝트 전반적으로 발생하는 다양한 Workflow를 구현할 수 있다.

**단점**

- Branch 수가 많다.
- 작업하기 약간 번거로울 수 있다.

---

<br>

## 🔍 저장소 개념

**중앙 원격(remote) 저장소**

- Organization으로 저장된 저장소
- 여러 명이 같은 프로젝트를 관리하는 데 사용하는 그룹 계정의 중립된 원격 저장소
- 사용자와 저장소는 팀으로 관리되고 저장소의 권한 설정도 팀으로 관리한다.

<br>

**자신의 원격(remote) 저장소**

- 인터넷이나 네트워크 어딘가에 있는 저장소
- remote repository 라고 불린다. (또는 origin)
- 파일이 GitHub 전용 서버에서 관리되는 원격 저장소

<br>

**로컬(local) 저장소**

- local repository 라고 불린다.
- 내 PC에 파일이 저장되는 개인 전용 저장소, 지역 저장소

---

<br>

**❗️여기서부터는 dongurami 서비스의 협업 방식인 gitflow workflow방식을 기반으로 설명되어 있습니다.** 

<br>

## 1️⃣ 로컬 저장소 생성하기

프로젝트 참여자는 git clone 명령어를 이용해 로컬 저장소를 생성할 수 있다. 

원격 저장소를 자신의 깃허브로 Fork한  뒤 git clone 명령어로 원격 저장소를 복제 해 자신의 로컬 저장소를 생성

그 후 원격 저장소의 레포와 로컬 저장소를 동기화 시켜주는 작업을 해준다. 

```bash
git clone [Fork해 온 주소]
git remote add upstream [Fork하기 전 중앙 원격 레포의 주소]
git pull upstream master
```

<br>

> fetch와 pull의 차이

- fetch: 원격 저장소의 데이터를 로컬에 가져오기만 하기
- pull: 원격 저장소의 내용을 가져와 자동으로 병합 작업을 실행

즉, 단순히 원격 저장소의 내용을 확인만 하고 로컬 데이터와 병합은 하고 싶지 않으면 fetch 명령어를 사용
pull = fetch + merge

---

<br>

## 2️⃣ 새로운 기능 개발을 위해 격리된 브랜치 생성

중앙 원격 저장소에는 master branch가 있고, develop branch 추가해 놓은 상태.

자신의 작업하려는 기능에 대한 branch 생성 ex) login

로컬 저장소에도 login branch를 따고, 작업을 진행한 뒤 커밋한다.

자신의 remote 저장소의  login branch로 push한 뒤 원격 저장소의 login branch로 PR 전송

---

<br>

## 3️⃣ 원격 저장소에서 병합

관리자가 PR 내용을 검토한 뒤 원격 저장소의 login branch로 merge 시킨다. 

그 후 한 번 더 develop 브랜치로 merge 시켜준다.

<br>

> **feature branch** 
- 각 기능을 맡은 팀원만 작업을 진행. 
- 기능 구현을 완료 하였으면 즉시 삭제

<br>

> **develop branch** 
- 각 기능들을 병합시켜 놓은 branch라고 볼 수 있다.
- 팀원들이 작업한 기능이 계속 업로드되어 내용이 변경되기 때문에 자신의 로컬에서 작업 시작 전에 원격 
   저장소의 develop branch에서 pull을 당겨와 변경된 내용을 적용한 뒤 작업을 수행해야 한다.

<br>

feature branch에서 모든 기능을 구현하고, develop branch로 병합을 시켜줬으면 

master bracnh로 최종 병합을 해준다. 

> **master branch**
- 서비스를 배포하기 위한 최종 branch

---

<br>

## ❗️주의 사항

만약 원격 저장소 develop branch에서 변경된 내용을 Pull 당겨온 뒤 새로운 feature branch를 따서 작업하던 중 develop branch가 merge되어 내용이 수정된 경우

⇒ 자신이 하던 작업을 완료한 뒤 일단 commit과 push를 한다. 그리고 다시 pull을 당겨오는데 만약 충돌이 난다면 해당 팀원과 상의한 뒤 내용을 수정해주면 된다. 

---

<br>

## 📝참고 자료

- Gitflow Workflow: [https://gmlwjd9405.github.io/2018/05/12/how-to-collaborate-on-GitHub-3.html](https://gmlwjd9405.github.io/2018/05/12/how-to-collaborate-on-GitHub-3.html)
- Feature Branch Workflow: [https://gmlwjd9405.github.io/2017/10/27/how-to-collaborate-on-GitHub-1.html](https://gmlwjd9405.github.io/2017/10/27/how-to-collaborate-on-GitHub-1.html)
