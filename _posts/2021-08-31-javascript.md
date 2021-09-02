---
title: "Javascript"
excerpt: "새로 배운 자바스크립트 문법 정리"

categories:
  - TIL
tags:
  - [javascript]

toc: true
toc_sticky: true

date: 2021-08-31
last_modified_at: 2021-08-31
---

## 자바스크립트 BOM(Browser Object Model)

- window: 브라우저 창
- location: 주소표시창
- history: 뒤로가기 앞으로 가기

## 기타 주요 메소드

- 새창 열기: window.open(url, wname, option);
- 하이퍼링크: location.href="..."
- 현재창 닫기: self.close
- 나를 열어준 창: opener

## Local Storage

- **브라우저에 유지**하는 저장소
- HTML5 API(JS)
- 전역개체인 window의 하위 객체: window.localstorage
- key-value 저장 , value에는 string 데이터만 저장가능, 도메인 별로 관리
- js의 객체를 json의 string으로 변경해서 저장
  Json.stringnify(obj):{name:'KJH', age:26} => "{name:'KJH', age:26}"
- local storage에서 값을 읽어올때는 string을 객체로 변환
  JSON.parse(str): "{name:'KJH', age:26}" => {name:'KJH', age:26}
- seamless(끊기지 않는, 네트워크 연결이 중단되어도 서비스가 가능한)
- 주요 메소드
  - setitem(key, value)
  - getitem(key)
  - removeItem(key)

* session storage는 tab별로 유지

## DOM(Document Objet Model)

브라우저에서 html파일을 읽을때 각 element들을 파싱하여 dom tree를 생성.
element들과 text는 node로 변환됨

### Node

- nodeType
  - 1: Element
  - 3: Text
- nodeName
  - Element: Tag 이름
  - Text: X
- NodeValue

  - Element: X
  - Text: text값

- text노드는 Element노드의 자식
- 속성노드는 하위노드는 아니지만 Element노드로부터 찾을 수 있음
- 공백도 노드로 만들어진다.

### DOM 탐색

- getElementById()
- getElementsByTagName()
- getElementsByClassName()
- querySelector()
- querySelectorAll()
- 속성을 사용한 탐색
  - xxx.childnodes
  - xxx.firstChild
  - xxx.lastChild
  - xxx.parent

### DOM 조작

xxx.appendChild()
xxx.removeChild()

## Event Handling

- User Event: 사용자의 action에 의한 Event
- Non-User Event: System, time 등의 사용자가 발생시키지 않는 Event

- Event: 사건, 일어난 정황
- Event Source: 사건을 일으킨 대상, 근원지
- Event Handler: 사건을 처리하는 대상

### Event 핸들링을 위한 구현 과정

1. UI 상에서 발생가능한 Event 유형 찾기
2. Event 유형마다 Event Handler 작성
3. Event Source에 Event Handler 등록

## Event Handler 작성법

1. inline 방식: `<div onclick="JS 문장">`(익명함수가 만들어지고 코드가 그 안에 들어간다.) => 가독성이 떨어지고 코드 재사용 불가
2. 분리된 함수로 작성하여 event source에 등록
   - xxx.on 속성 사용: 이벤트 타입당 하나의 이벤트 핸들러만 등록가능
   - addEventListener() 메소드 사용: 이벤트 타입당 복수의 이벤트 핸들러 등록 가능

## This

this는 기본적으로 자신의 상위 객체를 가르킴
기본적으로 windwo 객체를 가르치는데 onclick 등록을 script에서 하면 해당 객체를 자신을 호출한 객체로봄
