---
title: "코드리뷰"
excerpt: ""

categories:
  - ETC
tags:
  - [code review]

toc: true
toc_sticky: true

date: 2022-03-08
last_modified_at: 2022-03-08
---

## 코드리뷰란?
- 소프트웨어를 실행하지 않고 직접 검토하여 결함을 발견하고 개선하는 작업
- 개발 단계에서 일상적으로 수행하는 Daily Work

## 기대효과
- 결함 조기 검출
- 유지보수성 증대
- 역량강화
- 수평 문화
- 협업 개발

# 코드리뷰 방법론(오프라인)


1. Inspection
2. Technical Review
3. Walkthrough
4. Informal
- 아래로 갈 수 록 Informal

## Inspection
- 전문적 inspection team이 process와 checklist에 따라 Defect을 찾는 기법
    - 훈련된 진행자에 의해 진행
    - 시작/종료 조건을 갖는 체크리스트/규칙/프로세스가 존재
    - 전문가에 의한 정확성의 공식적 평가
    - 결함 발견이 목표

- R&R
    |역할|내용|
    |:--:|:--:|
    |Moderator|Inspection 진행 의장, 계획 및 Inspector 선정|
    |Author|검토 대상 산출물 작성자, 검토 결과 조치|
    |Reader|코드 및 문서 공유, 사전 리뷰 결과서 작성|
    |Inspector|검토 대상을 검토, 결함 발견, 결함해결보다는 의견 제시|
    |Recorder|Inspection시 나온 의견 기록, 문서화|

- 수행주체
    - QA 조직 내 inspection team 운영
    - 별도 컨설팅

- 수행방법
    - Planning-Overview-Preparation-Meeting-Rework-Follow up

## Peer Review
- 개발팀이 주도하여 직접 모여 수행하는 리뷰 기법
    - 정기적 리뷰
    - PL 또는 TL이 주도하여 리뷰대상 선정과 개발자에게 리뷰를 준비 요청
    - 리뷰는 발표자(개발자)가 리드하며, Wiki등을 사용하여 기록
    - Defect Management System(Jira 등)을 활용하여 업무 할당

- 수행방법
    - Author가 자신의 코드 설명, 팀원들은 결함과 개선안 찾는다.
    - Moderator는 리뷰 주제를 선정하고 결과를 정리해서 Action Item으로 기록

## Peer desk check
- Code commit 이전에 직접 모니터를 보면서 주변의 동료와 함께 짧은 시간 간단히 리뷰
    - 가장 쉽게 적용할 수 있는 리뷰 방식이며 실수 등을 쉽게 찾아낼 수 있어 의외로 효과가 좋은 방식
    - Build 여부, Unit Test 개발, 수행 여부, readability, commit 내용 및 message 확인 등
    - 다른 리뷰 기법과 병행하며 좋은 효과를 얻을 수 있음

## Weekthrough
- Peer Review와 유사하나 문서 작성자가 주도하는 가벼운 비정기적 아디이어 회의 형태
- 구성원들의 의욕이 없는 경우 효과 없음
- 일반적으로 QA팀에서 버그분석 등의 정보공유에 사용한다.

## Pass Around
- 작성자가 리뷰할 내용을 메일 또는 시스템을 통해 등록
- 참석자들이 메일이나 comment를 통해 의견 전달
- 강제성이 없어 속도가 느림

## Pair Programming
- 두명의 작업자가 한개의 PC를 공유하며 작업 하는 형태
    - Navigator가 작업방향 제시/ 목표점검/ 코드리뷰등을 수행, Driver가 키보드 소유하고 직접 개발 수행
- 수행목적
    - 팀내 커뮤니케이션 증진
    - 개발 역량 상향, 지식 굥유
    - 코드 품질 개선(표준화/ 가독성 향상)
    - 업무 집중도 향상
    - 업무 난이도가 높은 문제를 해결


# 코드리뷰 방법론(온라인)

1. Automated Peer code review
2. Modern code review

## Pre-commit Review
- 형상관리 시스템에 코드가 반영 전 리뷰 수행
- 장점
    - 코드 반영 전 점검 가능
    - 리뷰 활동이 강제됨(리뷰 안된 파일은 반영 불가)
    - 리뷰를 통한 결함 제거로 팀 개발 활동 보호
- 단점
    - 리뷰 완료 전 추가 작업 불가 -> 복수 리뷰어 참여 시 (리뷰 기간이 길 경우) 생산성 저하
    - 리뷰 통과 이후 개발자가(실수 or 의도적으로) 다른 코드 반영 가능

## Post-commit Review
- 형상관리 시스템에 코드가 반영 후 리뷰 수행
- 장점
    - 지속적인 코드 변경 사항 반영 가능
    - 다른 팀 멤버가 변경 사항을 바로 확인 및 조치 가능
    - 복잡한 요구사항 구현 시 편리 -> 여러 변경사항을 일단 반영 후 통합적 리뷰 가능
- 단점
    - 형상관리 시스템에 낮은 품질의 코드 유입 가능성 존재
    - 결함 발견시 작업 코드 롤백 필요

# 코드리뷰 운영 프로세스
한번에 완벽한 코드리뷰를 해야한다는 목표를 버려야함
1. 팀 목표 수립: 개발목표 및 팀 수준 고려
2. Gound rule 수립: 팀 목표를 위한 행동 양식
3. 수행 기법, 항목 및 checklist 수립
4. 시스템 및 정책 수립

## 코드리뷰가 어려운 이유
- 완벽한 코드는 존재하지 않는다.
    - 주위 상황에 따라 변경 가능
- 효율성 있는 코드리뷰의 명확한 기준의 기준과 방법을 정의하기 어려움
    - Checklist가 상세하고 자세한 경우 코드리뷰에 투입되는 시간이 증가
    - 개인별 개발능력이 상이하여 Checklist 이해수준이 달리짐
- 리뷰어의 도메인 지식 수준이 상이
    - 도메인 지식이 없으면 리뷰가 사실상 어렵거나 의견을 제시하기 힘듬
    - 특히 Defect 발견이 코드리뷰의 주목적이 되는 경우 리뷰는 더 어려워짐
- 개인의 특성 상이
    - 개인별 리뷰 포인트가 상이

## 코드리뷰 팀 목표 수립 범위 define
1. Readability
    - Understanding
    - Code Convention
2. Correctness(Testability)
3. Domain
4. Design Performance


## 코드리뷰 Ground Rule
### Author
- Self-Inspection
    - 리뷰 요청 전에 Clean Code 작성 확인
- Commit 작성
    - Commit, Pull Request는 단일 기능, 주제 단위로 작성
    - 1시간 내 리뷰를 고려하여 200 LOC 이하 권장
    - 코드 수정이 충분히 설명된 Commit Message 작성
- 리뷰요청
- 리뷰 의견에 대한 대응 및 조치 수행
- Merge 수행
    - 리뷰 의견 대응 및 조치 하였는지 판단 후 Merge 필요
### Reviewr
- 리뷰 관점
    - 툴로 검출이 어려운 로직 구조적 측면 집중
    - Commit 성격에 따른 리뷰 관점 차별화
- 리뷰 의견 작성
    - 작성된 코드에 대한 문제 제기, 문의는 Comment 작성
        - 질문, 문제의 검출/해결 방향을 구체적으로
        - 가능하면 부럽고 완곡하게
        - 리뷰 목적에 부합하지 않는 내용 작성 지양
        - 수정 범위가 아닌 코드에 대한 Comment 작성 지양


## Best Practice for code review
- 한번에 400 라인 이하의 코드를 리뷰
- 시간당 500 라인 정도의 코드를 리뷰
- 60분을 넘겨 리뷰 하지 않는다.

