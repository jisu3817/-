## ✔️ Husky

- git에 어떤 명령이 실행될 때 같이 실행하게 할 수 있는 명령을 관리하는 도구
- git commit을 할 때, 코드가 제대로 고쳐졌는지 검사해서 자동으로 바꿔주는 역할
- commit 실수를 줄일 수 있음.
- Git 2.13.0 이상 버전을 지원

### 🔎 사용 방법

1️⃣ husky 모듈 설치

```bash
$ npm install husky --save-dev
```

2️⃣ 커밋되기 전에 Husky가 검사할 내용에 대해서 package.json에 추가

```json
..., // 앞서 작성된 코드들 
"husky": { 
	"hooks": { 
		"pre-commit": "eslint . --fix && prettier --write"
	} 
} 
... // 이어 작성될 코드들
```

husky가 커밋 전에 실행되기 때문에 위처럼 pre-commit을 설정 해주면 커밋할 때 등록된 명령어를 실행하고   자동으로 고쳐지지 않으면 에러를 띄워 커밋이 되지 않게 만들 수 있다. 

`eslint . --fix` : 현재 디렉토리의 모든 코드를 eslint를 사용해 자동으로 고침.

`prettier --write` : prettier 규칙을 적용한 뒤 자동으로 고침.

**코드를 수정해야만 커밋이 가능한 환경이 설정** 

---

## ✔️ Lint-staged

- husky는 모든 코드를 다 검사하기 때문에 상당히 비효율적임.
- Lint-staged는 staging area에 들어간 코드들만 검사 해 효율적으로 코드 검사 가능.

### 🔎 사용 방법

1️⃣ Lint-staged 모듈 설치

```bash
$ npm install lint-staged --save-dev
```

2️⃣ package.json 수정

```json
..., // 앞서 작성된 코드들 
"lint-staged": { 
	"*.js": ["eslint . --fix", "prettier --write"] 
}, 
"husky": { 
	"hooks": { 
		"pre-commit": "lint-staged" 
	} 
}, 
... // 이어 작성될 코드들
```

커밋 메시지 작성 전에 lint-staged를 실행해 내용이 변경된 파일 중 `.js 확장자`로 끝나는 파일만 린트로 코드 검사를 수행 (변경, 추가 파일만 검사)
