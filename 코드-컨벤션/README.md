더 자세한 내용은 해당 링크 참고 

- Prettier Options: [https://prettier.io/docs/en/option-philosophy.html](https://prettier.io/docs/en/option-philosophy.html)
- ESLint RUles: [https://eslint.org/docs/developer-guide/working-with-rules](https://eslint.org/docs/developer-guide/working-with-rules)

## ESLint

ESLint는 JavaScript, JSX의 정적 분석 도구로 오픈 소스 프로젝트로 코드를 분석해 문법적인 오류나 안티 패턴을 찾아주고 일관된 코드 스타일로 작성하도록 도와준다. 

다양한 도구들이 있지만 ESLint가 커스터마이징이 쉽고, 확장성이 뛰어나 많이 쓰이고 있는 추세이다. 

 ESLint 스타일 가이드에는  Airbnb Style Guide, Google Style Guide 등이 있다. 

1. 코드 분석기로 코드의 문제를 찾아 준다.
2. 자동으로 수정될 수 있다.
3. 프로젝트 방식에 맞게 사용자 정의에 따라 고유한 규칙을 작성할 수 있다

## Prettier

Prettier는 기존의 코드에 적용되어있던 스타일을 전부 무시하고, 정해진 규칙에 따라 자동으로 코드 스타일을 정리해 주는 코드 포멧터이다.

ESLint에도 formatting 관련 규칙들이 있지만, Prettier는 formatting에 특화되어 있다.

EESLint는 문법 에러를 잡아내고, 특정 문법 요소를 쓰도록 만드는 등 코드 퀄리티와 관련된 것을 고치기 위해 사용되지만 Prettier는 코드 한 줄의 최대 길이나, 탭의 길이는 몇으로 할 것인지, 따옴표는 홀따옴표(')나 쌍따옴표(")중 무엇을 사용 할 것인지 등등 코드 퀄리티보단 **코딩 스타일을 일괄적으로 통일하는 도구**에 가깝다.

> Prettier를 활용해 자신이 작성한 코드를 정해진 코딩 스타일에 맞게 변환
ESLint를 활용해 자신이 작성한 코드 품질이 괜찮은지 검사 가능

⇒ **Prettier**와 **ESLint**를 같이 쓰면 코드 품질을 바로 잡은 뒤 코드를 정해진 코딩 스타일에 맞게 바꿀 수 있다.

---

### prettier와 ESLint 같이 사용하기

1. **Node Module 설치하기(eslint 모듈)**

```bash
$ npm install eslint --save-dev
```

package.json 파일의 dependencies에 eslint가 설치된 것을 확인한다.

1. **—init 명령어를 통해 eslint를 구성하고, .eslintrc 파일 생성하기**

```bash
$ eslint --init

? How would you like to use ESLint? 
=> To check syntax, find problems, and enforce code style

? What type of modules does your project use? 
=> CommonJS (require/exports) (바벨을 쓴다면 JavaScript modules)

? Which framework does your project use? 
=> None of these (react나 Vue를 사용한다면 그 해당 답변 선택)

? Does your project use TypeScript?
=> No(typescript 사용 x)

? Where does your code run? 
=> Node, Browser

? How would you like to define a style for your project? 
=> airbnb (보통 많이 사용 한다고 함. eslint:recommended + 개인 취향)

? What format do you want your config file to be in?
=>Json
```

위 명령어를 입력하고, 해당 질문에 대한 답변에 따라 .eslintrc 파일이 자동으로 생성된다. 

1. **prettier 모듈 설치**

```bash
$ npm install prettier --save-dev --save-exact
```

**버전이 달라지면서 생길 스타일 변화를 막을 수 있기 때문에** -save-exact 옵션이 추가

1. **필요한 추가 모듈**
- **eslint-config-prettier**: Prettier와 충돌할 설정들을 비활성화
- **eslint-plugin-prettier**: 코드 포맷할 때 Prettier를 사용하게 만드는 규칙 추가

**Prettier와 ESLint는 서로 충돌할 수 있기 때문에 eslint-config-prettier를 활용**

⇒ 프리티어와 충돌하는 ESLint 규칙을 끄는 역할

```bash
$ npm install eslint-plugin-prettier eslint-config-prettier --save-dev
```

.eslintrc.json파일에 다음과 같이 추가

```json
{ 
	"plugins": ["prettier"], 
	"extends": ["eslint:recommended", "plugin:prettier/recommended"], 
	"rules": { 
		"prettier/prettier": "error" 
	} 
}
```

---

### **vscode 설정하기**

해당 기능들의 설정을 바꿔주기 위해 eslint와 prettier 확장 프로그램을 vscode에서 설치 해준다. 

VS Code에서 파일을 저장할 때마다 자동으로 고쳐지게 설정하기

vscode 설정 → 우측 상단의 json으로 설정보기 → 다음과 같이 코드 수정/추가

```json
{ // Set the default 
	"editor.formatOnSave": false, 

	// Enable per-language 
	"[javascript]": { 
		"editor.formatOnSave": true 
	}, 
	"editor.codeActionsOnSave": { 

		// For ESLint 
		"source.fixAll.eslint": true 
	} 
}
```

---

### **.eslintrc.json 설정 파일 (자신의 사용 목적에 맞게)**

```json
{
  "extends": ["airbnb-base", "eslint:recommended", "plugin:prettier/recommended"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error",
    "no-undef": "off",
    "no-console": "off"
  },
  "ignorePatterns": ["node_modules/"],
  "parserOptions": {
    "ecmaVersion": 2021
  },
  "env": {
    "es6": true
  }
}
```

1. parserOptions (자바스크립트를 해석하는 파서의 설정)
    1. ecmaVersion : 자바스크립트의 버전 7 (es7 / ECMA 2016) 선택
    2. sourceType : import/export 사용 안 함
    3. ecmaFeatures : jsx를 허용 안 함 (default :fasle)

2. env : (미리 정의된 전역 변수에 무엇이 있는지 명시)
    1. browser : 브라우저에서 사용하는 document 같은 객체를 사용할 수 있게 합니다.
    2. node : node에서 console 같은 전역 변수를 사용할 수 있게 합니다.

3. rules : 적용할 규칙들

### **.prettierrc.json설정 파일**

.eslintrc.json과 같은 위치에 파일을 만들고, [Prettier의 옵션 문서](https://prettier.io/docs/en/options.html)에서 필요한 설정을 골라 넣음.

```json
{ 
	"trailingComma": "es5", 
	"tabWidth": 2, 
	"semi": true, 
	"singleQuote": true 
}
```
