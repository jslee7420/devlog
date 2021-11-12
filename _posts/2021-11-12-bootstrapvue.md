---
title: "BootstrapVue"
excerpt: "Vue에서 사용하는 Bootstrap"

categories:
  - TIL
tags:
  - [vue]

toc: true
toc_sticky: true

date: 2021-11-12
last_modified_at: 2021-11-12
---

Vue.js에서 사용 가능한 부트스트랩 라이브러리입니다. 기존 부트스트랩이 클래스 형태로 라이브러리를 제공한것과 다르게 BootstrapVue에서는 컴포넌트의 형태로 제공됩니다. 클래스가 복잡하게 적용되는 기존의 부트스트랩보다 컴포넌트명을 사용하는 부트스트랩뷰가 더 직관적이라서 쉽게 사용할 수 있다는 생각이 듭니다.

공식문서 : https://bootstrap-vue.org/

## BootstrapVue 설치시 주의 사항

npm 으로 bootstrapVue 설치시 공식문서에서는 다음과 같은 방식으로 설치할 것을 권장하고 있습니다.

```cmd
# With npm
npm install vue bootstrap bootstrap-vue

```

하지만 위 방식으로 설치하면 문제가 있습니다.

BootstrapVue 공식문서에서는 Bootstrap 4.5.3을 기준으로 설명을 하고 있지만

현재 최신 버전의 Bootstrap은 5버전이므로 BootstrapVue 공식문서를 보고 컴포넌트를 적용시키는 것이 어렵습니다.

따라서 다음과 같이 버전을 지정하여 설치하여야 합니다.

```cmd
npm install bootstrap@4.5.3 bootstrap-vue
```
