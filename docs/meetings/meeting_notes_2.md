---
layout: default
title: 1/18 정기 미팅
parent: Meetings
has_children: false
---

> 작성일: 2024-01-15  
> Written By: [ClayCat](https://github.com/claycat)

> Devdalus 프로젝트 첫번째 정기 미팅입니다
> 장소: 오프라인 (모 스터디룸)  
> 참석자 : 장수길, 김라온, 박성훈,  노소희

## 지난 회의에서 정하기로 한 것들 
<details>
<summary>PR 템플릿</summary>
<div markdown="1">
    ```
    ## 💜 TodoList
    -----
    - [x] ~ 기능 구현
    - [x] ~ 페이지 구조화 및 스타일링

    ## ✅ PR Point
    -----
    - 무슨 이유로 어떻게 코드를 변경했는지
    - 어떤 위험이나 우려가 발견되었는지
    - 어떤 부분에 리뷰어가 집중해야 하는지

    ## 😡 Trouble Shooting
    -----

    ## 👀 Screenshot / GIF / Link
    -----

    ## 📚 Reference
    -----
    - 구현에 참고한 링크 (필요한 경우만 작성하고 없으면 지우기)
    ```
</div>
</details>

<details>
<summary>Commit Convention</summary>
<div markdown="1">
    Feat:	새로운 기능 추가
    Fix:	버그 수정 또는 typo
    Refactor:	리팩토링
    Design:	CSS 등 사용자 UI 디자인 변경
    Comment:	필요한 주석 추가 및 변경
    Style:	코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우
    Test:	테스트(테스트 코드 추가, 수정, 삭제, 비즈니스 로직에 변경이 없는 경우)
    Chore:	위에 걸리지 않는 기타 변경사항(빌드 스크립트 수정, assets image, 패키지 매니저 등)
    Init:	프로젝트 초기 생성
    Rename:	파일 혹은 폴더명 수정하거나 옮기는 경우
    Remove:	파일을 삭제하는 작업만 수행하는 경우
</div>
</details>

## FrontEnd Tech Stack
* React
* TypeScript
* Styled-Component
* 추가적인 사항은 필요성 느껴질 경우 조사하여 비교 후 결정

## Backend Tech Stack
* Spring + SpringBoot
* JPA / H2 (Tests)

## 개발 프로세스
* 최소한의 MVP를 가진 프로토타입을 먼저 출시 후 부가적인 기능 추가
* 애자일 기반 스프린트

### 피그마 페이지 생성 및 디자인 + 요구사항 디벨롭

[피그마 링크](https://www.figma.com/file/VRJ222hDwdsSDZF6O64dfp?type=design)