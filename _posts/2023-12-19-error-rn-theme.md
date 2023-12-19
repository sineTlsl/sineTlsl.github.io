---
layout: post
title: "[Error] ReactNative styled-components theme 타입 인식 못하는 에러"
date: 2023-12-19 18:25:00 +900
lastmod: 2023-12-19 18:25:00 +900
categories: [Error, ReactNative]
tags: [Error, ReactNative, styled-components]
use_math: true
---

## 🔺 에러 발생 원인은?

공식문서에 있는 그대로 theme 타입을 지정해주었는데, any 타입 에러가 계속 발생하는 문제다. 도대체 어떤게 문제일까?

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/1da24aca-6f00-427e-8af8-0a65a3b7d2f1" width="90%" />
</p>

> 'props' 매개 변수에는 암시적으로 'any' 형식이 포함됩니다.
> {: .prompt-warning}

## ❓ 그럼 어떻게 해결해야할까?

공식문서에 나와있는 그대로 [DefaultTheme](https://styled-components.com/docs/api#create-a-declarations-file)을 지정해주었는데도 에러가 난다.

```tsx
// ./src/types/styled.d.ts
import "styled-components/native";

declare module "styled-components/native" {
  export interface DefaultTheme {
    colors: {
      mainBg: string;
      white: string;
      black: string;
      blacklight: string;
    };
  }
}
```

```tsx
// ./src/styles/theme.ts
import { DefaultTheme } from "styled-components/native";

const customTheme: DefaultTheme = {
  colors: {
    mainBg: "#59748e",
    white: "#FFFFFF",
    black: "#000000",
    blacklight: "#575757"
  }
};

export { customTheme };
```

그런데도 vscode에서만 에러가 발생하고, 동작하는 부분에선 아무런 에러가 발생하지 않는다. 내 vscode 상 문제인가?? 다른 사람들은 같은 방법으로 다 해결을 하였는데, 나만…. 나만 안된다…

```json
// tsconfig.json
{
  "extends": "@tsconfig/react-native/tsconfig.json",
  "compilerOptions": {
		...
    "strict": false
  },
}
```

`strict` 모드를 `false`로 수정하긴 해서 일단 vscode 상에서 에러는 해결하였다. 올바른 방법은 아니지만 우선적으로 급한 부분은 해결을 하였으니 사용해보는 걸로 하고.. 아직 내가 부족한 부분이 많은 것 같으니 아시는 분들은 답변 좀 부탁드립니다… 🙏🏻🙏🏻

**Reference**

[styled-components 공식 홈페이지](https://styled-components.com/docs/api#create-a-declarations-file)

[styled-components 에러해결 : DefaultTheme 형식에 속성이](https://sezzled.tistory.com/27)
