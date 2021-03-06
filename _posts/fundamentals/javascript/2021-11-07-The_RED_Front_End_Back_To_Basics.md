---
the valayout: post
title: The RED 프론트엔드 Back to the Basics - 1. 정체되지 않는 프론트엔드 개발자의 일하는 방식 
subtitle : The RED 프론트엔드 Back to the Basics 1
tags: [javascript]
author: Leena Kim
comments : true
---



# 1. 정체되지 않는 프론트엔드 개발자의 일하는 방식

## 1) Intro - 프론트엔드의 과거와 지금 

- 자신의 경력을 하나의 소설처럼 생각하라

- 개연성이 있으면 이상해보여도 길이 될 수 있다. 
- 경력을 따라가다보면 돈은 따라오게 되있다.

<br>

<br>

## 2) 프론트엔드 개발자의 정의와 성장

- 프론트엔드 개발자의 정의 : 어플리케이션이 사용자와 맞닿는 지점을 만들고 관리하는 사람. 

- ex) 카카오뱅크 : 처음부터 사용자 편의에 중점을 맞췄다. 

  <br>

**프론트엔드의 단점**

- 사용자가 당장 불편함을 느끼지 않게 해야하고, 배워야 할 것이 많다. 디자이너와 협업할 일이 많고, 비즈니스 로직도 다루다보니 백엔드 지식도 상당히 요구한다. 넓고 깊게 알아야한다. 
- 이젠 html5, css3 같은 명세는 이제 없다고 봐도 된다. 이들이 부진하게 개발되다보니 주요 개발사들이 모여 2014년에 최종 권고안이 발표되었고, 지금은 what w g 라는 곳에서 담당하고 있다. html은 버전이 사라지고 계속해서 변화하는 리빙 스탠다드가 되었다. html5는 가장 최근의 명세는 2020년이 되었다. 
- 이처럼, 시간이 지나면 계속해서 새로운 기능이 추가되고 옛 기능이 사라진다. 계속 공부하지 않으면 뒤쳐지는건 금방이다. 스스로 답을 찾고 혼자 공부하는 법을 익혀야 한다. 

**프론트엔드의 장점**

- 자바스크립트는 계속해서 성장하고, 점유율도 높다. 타입스크립트도 마찬가지. 자바스크립트처럼 다양한 분야에서 활용되는 언어는 없다. 
- 이제는 리액트 네이티브 전문 개발자를 채용하기도 한다. 
- 네이티브에 대한 지식이 없어도, html css js만 가지고도 앱을 개발하는 수준에 이르렀다. 일렉트론이 그 예시. 웹기술을 사용해서 가벼운 메모장 프로그램부터 게임까지 만들 수 있다. 
- 사용자와 가장 가까운 점에서 만난다. 서버에서 다듬어 화면에 보내주는 것, 디자이너가 잘 꾸며준 화면을 실제 웹화면으로 만들어내는것도 프론트엔드 개발자다. 
- 전체 서비스가 다운되는 심각한 일이 일어날 수 없다. 어지간한건 개발과 테스트에서 걸러지고, 일부 고객에 대한 트러블만 처리하면 된다. 

<br>

**공부 방법**

- 영역은 조금씩 늘려가되, 필요한 부분에서 깊이를 줘라. 네이버의 경우 겨우 30여개의 html 태그만 사용하고 있다. 일단, 공부할 범위를 축소하는게 중요하다. (=국영수 위주로 공부하라)
- 시간이 날 때마다 관련 공식 문서를 읽어라. (=교과서 위주로 공부하라) html은 모질라 웹사이트에서 제공한다. 한번에 완벽하게 읽기보단, 자주 조금씩 반복하여 읽어라. 한번에 깊이 읽으면 흥미를 잃기 쉽다. 
- 이것 저것 많이 경험해보라. jquery부터 리액트까지. 기업에서는 항상 경력자를 찾는다. 어떤 프레임웤이나 기술을 얼만큼 능숙하게 다뤄봤는지가 중요하기 때문이다. 코드를 많이 읽고, 개인 프로젝트를 하라. 
  - 코드읽기 : 실무에서는 기술보다는 해당 업무에서만 사용되는 도메인 지식이 절대적으로 중요하다. 어떻게 코드를 작성할줄은 알겠는데, 이 코드가 원하는 것을 달성하도록 만드는것이 어렵다. 이 때, 다른 사람의 코드를 보는 능력이 있으면 쉽게 배울 수 있다. 
  - 개인 프로젝트 : 프레임워크도, 인기있는 기술도 사용해보라. 내 분야와 전혀 상관 없는 기술을 사용할때도 좋다. 프로젝트는 당장 지금 나에게 유용한 것을 만드는게 좋다. 끝까지 완성할 동기가 된다. 프로젝트 아이디어는 항상 메모해두라. 프로그래밍 언어는 눈으로 보는것과 실제로 사용해보는것이 다르다. 회사에서 기회를 얻긴 힘들 수 있으니 개인 프로젝트를 활용하라. 
- 어느정도 알고있는 기술이라면 글로 남겨보라. 잘 알고있는 기술이라고 생각했는데 글로 쓰거나 다른사람에게 설명하다보면 어려울 수 있다. 글로 남기면 머리에 오래 남는다. 
  - TIP 1. 정확한 지식만을 전달한다. 아주 짧은 책을 쓴다고 생각하라. 
  - TIP 2. 자료를 첨부하라.
  - TIP 3. 문장을 짧고 명확하게 하라. 

<br>

**빨리 변하는 프론트엔드 기술 습득법**

- 깃허브의 트렌딩 페이지를 자주 본다. 3분 미만이면 다 볼 수 있다. 오늘 가장 많은 관심을 받은 프로젝트를 보여준다. 재밌어 보이는 프로젝트의 제목과 간략한 설명을 보라. 그러다 보면 트렌드처럼 계속 눈에 띄는 프로젝트가 있을 것이다. 
- 트위터의 유명한 프론트엔드 계정을 팔로우하고 구독하라. 특정 기술이 계속 눈에 띌 것이다. 해외트렌드를 알 수 있다. 
- 채용공고를 꾸준히 읽어보라. 채용공고에 보인다는건 해당 프로젝트가 기업 시장에도 받아들여졌다는 것이다. 

<br>

**프론트엔드 개발자의 협업**

- 일정을 예측하기가 어렵다. 결과물에 시각적인 요소가 많기때문에 문외한도 의견을 낼 수 있다. 디자이너와 사용자가 협업을 할 일이 많다. 자주 사용하는 스타일은 컴포넌트로 만들어놓으라. 
- MVP, 즉 실행가능한 최소 단위의 프로젝트를 만들어보라. 피드백이 많기때문에 꼭 필요한 부분만 구현하고 의견을 받고 수정하라. 
- 백엔드 개발자와 API를 협의할 땐 백엔드 개발자가 데이터를 넘겨주기 용이하도록 협의해야 한다. 
- 안된다는 말은 가능하면 참아라. 개발자는 빠르게 가능한 조건을 파악해서 된다, 안된다로 얘기하곤 한다. 본인은 현실적으로 이야기한건데 자칫하면 부정적인 사람으로 비추어질 수 있다. 이 때, 안된다는 말 대신 조건과 요건을 변경하면 가능하다고 말하라. 안된다고만 말한다면 협업하기 힘든 개발자로 낙인이 찍힐 수 있다.

<br>

<br>

