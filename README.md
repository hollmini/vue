Vue.js
======

## Index
1. [Vue.js 소개]()
2. [Setting]()
3. 

## Vue.js 소개
Augular와 React에 비해 간단하지만 우수하고 빠르며, 
앵귤러의 데이터 바인딩 특성과 리액트 가상 DOM 기반 렌더링 특징을 모두 가지고 있다.
MVVM(Model - View - ViewModel)로 구조화하여 개발하는 방식이다.

### 컴포넌트 기반 프레임워크
뷰의 또 다른 큰 특징은 컴포넌트(Component) 기반 프레임 워크라는 점이다.
레고를 조립하듯 컴포넌트를 조합하여 화면을 구성 할 수 있다.
이 방식의 장점은 코드를 재사용 하기가 쉽다는 점이며, HTML 코드에서 화면의 구조를 직관적으로 파악할 수 있다.

### 리액트와 앵귤러의 장점을 가진 프레임워크
뷰는 앵귤러의 양방향 데이터 바인딩(Two-way Daga binding)과 리액트의 단방향 데이터 흐름(One-way Daga Flow)의 장점을 모두 결합한 프레임워크이다.

## Setting
1. Editer 설치
2. Node.js 설치 (nodejs.org)
	Current 버전보다 안정적인 LTS(Long Term Support) 버전을 설치하는것이 라이브러리 호환성 관점에서 더 좋다.
3. Vue devtools 설치
	뷰로 개발할때 도움을 주는 도구.	웹 앱의 구조를 간편하게 디버깅하너가 분석할 수 있으며 크롬, 파이어폭스, 사파리에서 모두 지원 된다.

## 뷰 인스턴스
1. 생성
<pre>
	<code><div id="app"><p>{{message}}</p></div></code>
</pre>
