---
title: "Secure Coding"
excerpt: "정보보안은 개발단계에서부터"

categories:
  - 보안
tags:
  - [보안]

toc: true
toc_sticky: true

date: 2021-11-13
last_modified_at: 2021-11-13
---

# 1. 시큐어(secure coding) 코딩이란?

개발자의 실수나 논리적 오류로 인해 SW에 내포될 수 있는 보안취약점을 배제하여 안전한 소프트웨어를 개발하는 SW개발 기법

# 2. 시큐어 코딩 가이드

취약점을 모두 고려하는 프로그래밍이란 어려운 일.

어떠한 규칙에 따라 코딩을 하면 되는지에 대한 기준이 있으면 좋을 것.

국내에서는 2012년 12월부터 행정안전부에 의해 시큐어 코딩에 대한 법규가 제정, 시행되어 그 기준을 제시 중(대한민국의 모든 행정기관 및 공공기관 정보시스템은 해당 가이드 준수 의무가 있음)

50개의 소프트웨어 보안 약점 항목으로 구성

JAVA 시큐어코딩 가이드 문서 다운로드 링크: https://www.kisa.or.kr/public/laws/laws3_View

## 1. 입력데이터 검증 및 표현

- 프로그램 입력값에 대한 검증 누락 또는 부적절한 검증, 데이터의 잘못된 형식 지정으로 발생하는 보안 약점.
- SQL 삽입, 자원 삽입, 크로스사이트 스크립트 등 26개 항목 존재
- 폼 양식의 입력란에 입력되는 데이터로 인해 발생하는 문제를 예방하기 위해 점검하는 보안 항목으로 주로 SQL Injection 공격을 막기 위한 코딩
- 자세한 내용은 Database SQL Injection관련 글 참고

## 2. 보안기능

- 보안인증(인증, 접근제어, 기밀성, 암호화, 권한관리 등)을 적절하지 안헥 구현시 발생할 수 있느 보안약점.
- 부적적한 인가, 중요정보 평문 저장 또는 전송 등 24개 항목 존재
- 주로 암호와 같이 중요한 정보를 암호화 없이 저장하거나 프로그램 내부에 하드 코딩되어 노출의 위험성이 있거나 인증과 권한 관리를 부적절하게 구현할 시 보안에 문제가 발생
- 보안 기능은 비인가 접근을 방어하고 저장된 정보를 암호화하여 취약한 기능이 존재하지 않도록 하는 것이 중요

### 적절한 인증 없는 중요기능 허용

```java
// 안전하지 않은 코드 예
// 재인증을 거치지 않는 계좌 이체
public void sendBankAccount(String accountNumber,double balance){
  ...
  BankAccount account = new BankAccount();
  account.setAccountNumber(accountNumber);
  account.setToPerson(toPerson);
  account.setBalance(balance);
  AccountManager.send(account);
  ...
}
```

```java
// 안전한 코드 예
// 인증 받은 사용자만이 다시 재인증을 거쳐 계좌 이체
public void sendBankAccount(HttpServletRequest request, HttpSession session, String
accountNumber,double balance){
  ...
  // 재인증을 위한 팝업화면을 통해 사용자의 credential을 받는다.
  String newUserName = request.getParameter("username");
  String newPassword = request.getParameter("password");
  if ( newUserName == null || newPassword == null ){
    throw new MyEception("데이터오류");
  }

  // 세션으로부터 로그인한 사용자의 credentail을 읽는다.
  String password = session.getValue("password");
  String userName = session.getValue("username");

  // 재인증을 통해서 이체여부를 판단한다.
  if ( isAuthenticatedUser() && newUserName.equal(userName) && newPassword.equal(password) ) {
    BankAccount account = new BankAccount();
    account.setAccountNumber(accountNumber);
    account.setToPerson(toPerson);
    account.setBalance(balance);
    AccountManager.send(account);
  }
  ...
 }
```

## 3. 시간 및 상태

- 동시 또는 거의 동시 수행을 지원하는 병렬 시스템, 하나 이상의 프로세스가 동작하는 환경에서 시간 및 상태를 부적절하게 관리하여 발생할 수 있는 보안약점
- 경쟁조건, 제어문을 사용하지 않는 재귀함수 등 7개 항목 존재
- Race Condition 이나 종료되지 않는 반복문이나 재귀문을 사용하여 무한루프에 빠지는 것 등이 시간 및 상태 점검 항목에 포함
- OS Race Condtion과 동기화 처리 관련 부분 참고

## 4. 에러 처리

- 에러를 처리하지 않거나, 불충분하게 처리하여 에러정보에 중요정보(시스템 등)가 포함될 때 발생할 수 있는 보안약점.
- 취약한 패스워드 요구조건 오류메세지를 통한 정보노출 등 4개

### 오류 메세지를 통한 정보 누출

종종 개발자가 디버깅의 편의성을 위해 에러 메시지를 화면에 출력하는 경우가 있다. 에러 메시지는 시스템과 관련된 중요 정보를 포함하는 경우가 많아 공격자의 악성 행위를 도울 수 있다. 또한, 오류가 발생할 상황을 적절하게 검사하지 않았거나 잘못된 처리를 한 경우도 에러 처리 항목에 포함된다. 에러 처리는 가능한 최소한의 정보만을 담고 있어야 하며, 광범위한 예외 처리보다는 구체적인 예외 처리를 통해 보안 공격을 사전에 방어하는 것이 중요하다.

```java
// 안전하지 않은 코드
// 예외 이름이나 스택 트레이스를 출력하면 프로그램 내부 정보가 유출된다.
public static void main(String[] args){
  String urlString = args[0];
  try{
    URL url = new URL(urlString);
    URLConnection cmx =
    url.openConnection();
    cmx.connect();
  }catch (Exception e){
    e.printStackTrace();
  }
}
```

```java
// 안전한 코드
// 예외 이름이나 스택 트레이스를 출력하지 않는다.
public static void main(String[] args){
  String urlString = args[0];
  try{
    URL url = new URL(urlString);
    URLConnection cmx = url.openConnection();
    cmx.connect();
  }catch (Exception e){
    System.out.println("연결 예외 발생");
  }
}
```

## 5. 코드오류

- 타입변환 오류, 자원(메모리 등)의 부적절한 반환 등과 같이 개발자가 범할 수 있는 코딩오류로 인해 유발되는 보안 약점
- 널 포인터 역참조, 부적절하나 자원 해제 등 7개
- 주로 형(Type) 변환 오류, 자원 반환, NullPointer 참조가 이에 해당한다. Null 값을 체크하지 않고 변수를 사용한다든가 실수로 스레드와 같은 자원을 무한하게 할당하여 시스템에 부하를 주는 경우가 있다.

### 널(NULL)포인터 역참조

일반적으로 특정 객체가 Null이 될 수 없다는 가정을 위반할때 발생

```java
// 안전하지 않은 코드
....
public void checknull(){
  String cmd = System.getProperty("cmd");
  // cmd가 null인지 체크하지 않음
  cmd = cmd.trim();
  System.out.println(cmd);
....
```

```java
// 안전한 코드
....
public void checknull(){
  String cmd = System.getProperty("cmd");
  // cmd가 null인지 체크
  if (cmd != null){
    cmd = cmd.trim();
    System.out.println(cmd);
  }else System.out.println("null command");
....
```

## 6. 캡슐화

- 중요한 데이터 또는 기능성을 불충분하게 캡슐화하였을 때, 인가되지 않는 사용자에게 데이터 노출이 가능해지는 보안약점
- 제거되지 않고 남은 디버그 코드, 시스템 데이터 정보노출 등 8개
- 부적절한 캡슐화는 정보은닉의 기능을 잃어버린다. 시스템의 중요 정보가 노출되어 공격자는 이 정보를 이용해 식별 과정을 우회할 수 있다. 변수 제어 함수가 노출된다면 공격자는 원하는 값으로 데이터를 외부에서 수정할 수 있게 된다.

### Public 메소드로부터 반환된 private 배열

```java
// 안전하지 않은 코드
// private배열을 public 메소드가 return
// private 배열의 레퍼런스를 얻을 수 있게됨
private String[] colors;
public String[] getColors() { return colors; }
...
```

```java
// 안전한 코드
....
private String[] colors;
// 메소드를 private으로 하거나, 복제본을 반환하거나, 수정을 제어하는 public 메소드를 별도로 만든다.
public String[] getColors(){
String[] ret = null;
  if ( this.colors != null ){
    ret = new String[colors.length];
    for (int i = 0; i < colors.length; i++) {
      ret[i] = this.colors[i];
    }
  }
  return ret;
}
....
```

## 7. API 오용

- 의도된 사용에 반하는 방법으로 API를 사용하거나, 보안에 취약한 API를 사용하여 발생할 수 있는 보안약점
- DNS Lookup에 의존한 보안결정, 널 매개변수 미조사 등 7개
- 만약 공격자에 의해 로컬 DNS 캐시가 오염된 상황에서 DNS만 확인한다면 공격자의 네트워크로 경유하거나 공격자의 서버를 도착지로 인식할 수 있다. 이를 방지하기 위해 보안에 취약한 API 사용은 피해야 하며 DNS가 아닌 IP를 확인하는 것이 중요

### DNS lookup에 의존한 보안 결정

```java
// 안전하지 않은 코드
// DNS 이름을 통해 해당 요청이 신뢰할 수 있는지를 검사하는 경우
// 공격자가 DNS 캐쉬를 조작하면 잘못된 신뢰 상태 정보를 얻게 됨
public class checkDNS extends HttpServlet
{
  public void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException){
    boolean trusted = false;
    String ip = req.getRemoteAddr();
    // 호스트의 IP 주소를 얻어온다.
    InetAddress addr = InetAddress.getByName(ip);

    // 호스트의 IP정보와 지정된 문자열(trustme.com)이 일치하는지 검사한다.
    if (addr.getCanonicalHostName().endsWith("trustme.com")){
      trusted = true;
    }
    if (trusted){
      ....
    }else{
      ....
    }
  }
}
```

```java
// 안전한 코드
// DNS lookup에 의한 호스트 이름을 비교하지 않고 IP 주소를 직접 비교
public class checkDNS extends HttpServlet{
  public void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException){
    String ip = req.getRemoteAddr();
    if (ip == null || "".equals(ip))
      return ;

    String trustedAddr = "127.0.0.1";

    if (ip.equals(trustedAddr)){
      ....
    }else{
      ....
    }
  }
}
```
