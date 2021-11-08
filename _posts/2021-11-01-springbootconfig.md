---
title: "Springboot 프로젝트 서버에 올리기"
excerpt: ""

categories:
  - TIL
tags:
  - [spring, springboot]

toc: true
toc_sticky: true

date: 2021-11-01
last_modified_at: 2021-11-01
---

스프링 부트 프로젝트는 jar와 war 두가지 파일로 압축할 수 있음
JAR (Java Archive) WAR (Web Application Archive) 모두 JAVA의 jar 툴을 이용하여 생성된 압축(아카이브) 파일이며 어플리케이션을 쉽게 배포하고 동작시킬 수 있도록 있도록 관련 파일(리소스, 속성파일 등)들을 패키징해주는 것이 주 역할

- jar

  - main 메소드가 있는 자바 어플리케이션 형태
  - JRE(Java Runtime Environment)만 가지고도 실행이 가능

- war
  - servlet / jsp 컨테이너에 배치 할 수 있는 웹 어플리케이션(Web Application) 압축 파일 포맷
  - WEB-INF 및 META-INF 디렉토리로 사전 정의 된 구조를 사용하며 WAR파일을 실행하려면 Tomcat, Weblogic, Websphere 등의 웹 서버 (WEB)또는 웹 컨테이너(WAS)가 필요

WAS에 올려서 배포하기 위해서는 war 파일로 만들어서 배포 해야함.

## 배포 과정

1. 프로젝트 마우스 우클릭
2. Run AS
3. 5 Maven build...
4. 프로젝트 디렉토리 안에 war 파일 생성
5. war 파일을 tomcat의 apache-tomcat-9.0.52/webapps 위치에 두기
6. ROOT 디렉토리 삭제
7. war 파일명 ROOT로 변경
8. apache-tomcat-9.0.52/bin/startup.bat 실행(deploy)
