## Eslint-Prettier

#### 목적

Eslint, Prettier 사용 예제 및 Vscode 환경 구성 작성

#### 공식 문서

[문서 사이트](https://eslint.org/docs/user-guide/configuring/)

#### 의존성 설치 (초기 설정할 경우 참고)

```bash
    yarn add eslint -dev
    yarn add prettier -dev
    yarn add eslint-plugin-prettier -dev # eslint prettier 세팅용
    yarn add eslint-config-prettier -dev # eslint & prettier 설정 충돌 방지

```

#### 시작하기

```bash
    yarn install
    npx eslitnt --init # eslint 환경 구성
    # npx는 실행 파일을 경로를 지정하지 않고 실행할 수 있게 도와주는 명령어
    ## npx 사용하지 않을 경우 ./node_modules/eslint/.bin/eslint --init 이런 식으로 구동해야함.
```

#### 시나리오

```javascript
// - index.js
const aB = 3; // 변경 전
const a_b = 3; // 변경 후

// npm lint 실행 => error 발생

// - .eslintrc.json파일의 rules 옵션 중 camelcase 옵션 "error" -> "off"로 변경

// npm lint 실행 => 정상 동작

// - .eslintrc.json파일의 camelcase 옵션 "off" -> "error" 변경

const a_b = 3; // 변경 전
const aB = 3; // 변경 후

// - index.js 파일의 불필요한 탭 추가

// npm lint:fix 실행 => 탭 자동 정렬 됨.
```

#### ESLint Configure 옵션

-   `Environments`: global variables 설정하는 옵션

```javascript
    /* true, false 설정. default = false */
    "env": {
        "browser": true,
        "es2021": true,
        "jest": true,
    },
    /*
        browser
        node
        commonjs
        es6
        es2017
        es2020
        es2021
        worker
        amd
        mocha
        jest
        qunit
        jquery
        shelljs ... 등등
    */
    /* ... */
```

-   `parserOptions`: ESLint 사용을 위해 지원하려는 Js 언어 옵션 지정

    -   ecmaVersion: 사용할 ECMAScript 버전을 설정
    -   sourceType: parser의 export 형태를 설정
    -   ecmaFeatures: ECMAScript의 언어 확장 기능을 설정
    -   [ECMA란?](https://sumini.dev/til/006-ecmascript/)

-   `parser`: ESLint 구문 분석을 위해 사용되는 `parser`설정 `default = 'Espree'`

    -   babel용 파서 `babel-eslint`, typescript용 파서 `@typescript-eslint/parser`

-   `plugin`: ESLint는 서드파티 플러그인 사용을 지원한다. 해당 플러그인을 설정할 수 있는 옵션이다.

-   `extends`: ESLint 서드파티로 추가한 플러그인에서 사용할 규칙을 설정해주는 옵션
    -   뒤에 오는 설정이 앞의 설정을 덮어쓰기때문에 순서를 잘 넣어줘야한다.

```javascript
    /*  */
    "plugins": ["@typescript-eslint", "import"],
    "extends": [
        "plugin:@typescript-eslint/recommended",
        "airbnb-typescript",
        "plugin:import/errors",
        "plugin:import/warnings",
        "plugin:import/typescript",
    ],
```

-   `rules`: ESLint가 프로젝트에 사용할 규칙을 설정할 수 있는 곳
    -   `off` or `0`: 규칙을 사용하지 않음
    -   `warn` or `1`: 규칙을 경고로 사용
    -   `error` or `2`: 규칙을 오류로 사용
    -   규칙에 추가 옵션이 있는 경우 배열 리터럴 구문을 사용하여 지정 가능

[Rules]

```javascript
{
	"rules": {
		"eqeqeq": "off",
		"curly": "error",
		"quotes": ["error", "double"],
		"comma-style": ["error", "last"]
	}
}
```

-   인라인으로 룰 적용 방지

```javascript
// 경고 비활성화 블록 주석
/* eslint-disable */
alert('foo');
/* eslint-enable */
```

-   특정 파일 그룹에 대해서만 규칙 비활성화

```javascript
 "overrides": [
    {
      "files": ["*-test.js","*.spec.js"],
      "rules": {
        "no-unused-expressions": "off"
      }
    }
```

-   파일 디렉토리 제외
    -   `ignorePatterns` 혹은 `eslintignore` 파일 작성하여 제외 가능

```javascript
// .eslintrc 파일 ignorePatterns 설정
{
	"ignorePatterns": ["temp.js", "node_modules/"],
	"rules": {
		//...
	}
}
```

#### ESLint + Prettier + Vscode

[참조 문서](https://sunmon.github.io/vscode-eslint-prettier-setting/)

```bash
    # ESLint extension 설치
    # ( ctrl + shift + p ) => 명령 팔레트 열고
    # > format document (문서 서식 프로그램) 클릭
    # 기본 포맷터 prettier로 설정

```

```javascript
    // vscode의 setting.json을 열고
    {
        /* ... */
        "editor.formatOnSave": true, // <- 추가해줘야 저장할 때 반영 됨
        /* ... */
    }
```
