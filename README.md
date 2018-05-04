Vue.js
======

## Index
1. [Vue.js 소개]()
2. [Setting]()
3. [뷰 인스턴스]()
4. [뷰 컴포넌트]()
4. [뷰 라우터]()

## Vue.js 소개
Augular와 React에 비해 간단하지만 우수하고 빠르며, 앵귤러의 데이터 바인딩 특성과 리액트 가상 DOM 기반 렌더링 특징을 모두 가지고 있다. MVVM(Model - View - ViewModel)로 구조화하여 개발하는 방식이다.
또 다른 큰 특징은 **컴포넌트(Component) 기반 프레임 워크**라는 점인데, 레고를 조립하듯 컴포넌트를 조합하여 화면을 구성 할 수 있다.
이 방식의 장점은 코드를 재사용 하기가 쉽다는 점이며, HTML 코드에서 화면의 구조를 직관적으로 파악할 수 있다.
 뷰는 앵귤러의 **양방향 데이터 바인딩(Two-way Daga binding)**과 리액트의 **단방향 데이터 흐름(One-way Daga Flow)**의 장점을 모두 결합한 프레임워크이다.

## Setting
- **Editer** 설치
- **Node.js** 설치 : [nodejs.org](https://nodejs.org/en/)
- **Vue devtools** : 뷰로 개발할때 도움을 주는 도구. 앱의 구조를 간편하게 디버깅하너가 분석할 수 있으며 크롬, 파이어폭스, 사파리에서 모두 지원 된다.

> **TIP** : node.js는 Current 버전보다 안정적인 LTS(Long Term Support) 버전을 설치하는것이 라이브러리 호환성 관점에서 더 좋다.

## 뷰 인스턴스
### 기본 생성 
```
<div id="app">
	<p>{{message}}</p>
</div>
<script type="text/javascript">
	new Vue({ // 인스턴스 생성
		el: '#app', // DOM 요소 지정
		data: { // data 값 정의
			message: 'Hellow world'
		}
	})
<script>
```

> ※ example : 01_vue_Instance.html

### 관련 속성
- template : 화면에 표시할 HTML, CSS 등의 마크업 요소를 정의하는 속성, 뷰의 데이터 및 기타 속성들도 함께 화면에 그릴 수 있음
- methods : 화면 로직 제어와 관계된 메서드를 정의하는 속성이며 마우스 클릭 이벤트 등의 전반적인 이벤트 등화면 동작과 관련되 로직을 추가
- created : 뷰 인스턴스가 생성되자마자 실행할 로직을 정의할 수 있는 속성

### 라이프 사이클
인스턴스의 상태에 따라 호출할 수 있는 속성이 라이프 사이클(life cycle)이며, 각 속성에서 실행되는 커스텀 로직을 라이플 사이클 훅(hook)이라고 한다. 라이플 속성에는 created, before Create, beforeMount, mounted 등 인스턴스의 생성, 변경, 소멸과 관련되어 총 8개가 존재한다.

#### 라이프 사이클의 단계
라이프 사이클의 단계를 크게 나누면 **생성**, 생성된 인스턴스를 화면에 **부착**, 화면에 부착된 인스턴스의 내용 **갱신**, 인스턴스가 제거되는 **소멸**, 4가지로 이루어져 있다. 부착 → 갱신 구간은 데이터가 변경되는 경우에만 거치게 되며, 각 단계 사이에 위에서 언급된 라이프 사이클 속성들이 실행된다.
1. **beforeCreate** : 인스턴스가 생성 된 후 가장 처음 실행되는 라이프 사이클 단계이며, data 속성과 methods 속성이 아직 정의되어 있지 않고, DOM에도 접근할 수 없다.
2. **created** : beforeCreate 다음으로 실행되는 단계로, data 속성과 methods 속성이 정의되어 this.data 또는 this.fetchData()와 같은 로직들을 실행할 수 있다. 하지만 아직 인스턴스가 화면에 부착되기 전이기 때문에 template 속성에 정의된 돔 요소로 접근할 수는 없다.
3. **beforeMount** : created 단계 이후 template 속성에 지정한 마크업 속성을 랜딩(부착)하기 전에 호출되는 단계이다.
4. **mounted** : el 속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 호출되는 단계로, template 속성에 정의한 DOM에 접근할 수 있어 화면 요소를 제어하는 로직을 수행하기 좋은 단계이다. 다만 돔에 인스턴스가 부착되자마자 바로 호출되기 때문에 하위 컴포넌트나 외부 라이브러리에 의해 추가된 화면 요소들이 HTML코드로 변환되는 시점과 다를 수 있다.
5. **beforeUpdate** : el 속성에서 지정한 화면 요소에서 인스턴스가 부착되고 나면 인스턴스에 정의한 속성들이 화면에 치환된다. 치환된 값은 뷰의 반응성을 제공하기 위해 $watch 속성으로 감시되며, 이를 **데이터 관찰** 이라고 한다. 또한 beforeUpdate는 관찰하고 있는 데이터가 변경되면 가상 돔으로 화면을 다시 그리기 전에 호출되며, 변경 예정인 새 데이터에 접근할 수 있어 변경 예정 데이터의 값과 관련된 로직을 미리 넣을 수 있다.
6. **updated** : 데이터가 변경된 후 가상 돔으로 화면을 다시 그리고 나서 실행되는 단계이다. 데이터 변경으로 인한 화면 요소 변경까지 완료된 시점이므로, 데이터 변경 후 화면 요소 제어와 관련된 로직을 추가하기 좋은 단계이다. 해당 단계에서 데이터 값을 변경하면 무한 루프에 빠질 위험성이 있어 computed, watch와 같은 속성을 사용해야 한다. 따라서 데이터 값을 갱신해야 하는 로직은 가급적이면 beforeUpdate에 추가하고, updated에서는 변경 데이터의 화면 요소(돔)과 관련된 로직들을 추가하는것이 좋다.
7. **beforeDestroy** : 인스턴스가 파괴되기 적전에 호출되는 단계이다. 이 단계에서는 아직 인스턴스에 접근할 수 있으며, 인스턴스의 데이터를 삭제하기 좋은 단계이다.
8. **destoryed** : 인스턴스가 파괴되고 난 후 호출되는 단계이다. 인스턴스에 정의한 모든 속성이 제거되고 하위에 선언한 인스턴스들 또한 모두 파괴된다.

> ※ example : 02_lifecycle.html

## 뷰 컴포넌트
### 컴포넌트(Component)란?
조합하여 화면을 구성할 수 있는 블록을 의미한다. 컴포넌트를 활용하면 빠르게 구조화하여 일괄적인 패턴으로 개발이 가능하며, 코드 재사용이 훨씬 편리해진다. 또한 모든 사람들이 정해진 방식대로 컴포넌트를 등록하거나 사용하게 되므로 남이 작성한 코드를 직관적으로 이해할 수 있다.

### 컴포넌트 등록 형식
등록 방법은 **전역(Global)**과 **지역(Local)** 두가지가 있는데, 지역 컴포넌트는 특정 인스턴스에서만 사용할 수 있고, 전역 컴포넌트는 여러 인스턴스에서 공통으로 사용 할 수 있다.

```
<div id="app">
	<p>첫번째 인스턴스 영역</p>
	<!-- 전역 컴포넌트 태그 추가 -->
	<global-component></global-component>
	<!-- 지역 컴포넌트 태그 추가 -->
	<local-component></local-component>
</div>
<script type="text/javascript">
	Vue.component('global-component', { // 전역 컴포넌트 등록
		template: '<div>전역 컴포넌트가 등록되었습니다.</div>' // 전역 컴포넌트 내용
	})
	var cmp = { // 지역 컴포넌트 내용
		template: '<div>지역 컴포넌트가 등록되었습니다</div>'
	}
	new Vue({
		el: '#app',
		components: { // 지역 컴포넌트 등록
			'local-component': cmp 
		}
	})
</script>

> ※ example : 03_component.html
```
### 뷰 컴포넌트 통신
컴포넌트 간 유효 범위로 인해 다른 컴포넌트의 값을 직접 접근하지 못하기 때문에 일관된 구조로 애플리케이션을 작성해야 한다. 이에따라 개발자 개개인의 스타일대로 구성되지 않고 애플리케이션이 모두 동일한 데이터 흐름을 갖게 되어 다른사람의 코드도 빠르게 파악할 수 있어 협업하기 수월해진다. 컴포넌트끼리 통신을 원하면 뷰 프레임워크 자체에서 정의한 컴포넌트 데이터 전달 방법을 따라야 한다.

#### 상위 컴포넌트(인스턴스)에서 하위 컴포넌트로 데이터 전달
**props**는 상위 컴포넌트에서 하위 컴포넌트로 데이터를 전달할 때 사용하는 속성이다. props속성을 사용하려면 먼저 하위 컴포넌트의 속성에 정의한다.
다음 단계로 로 상위 컴포넌트의 HTML 코드에 등록된 컴포넌트 태그에 v-bind 속성을 추가한다.
v-bind 속성의 왼쪽 값으로 하위 컴포넌트에서 정의한 props속성을 넣고, 속성 값으로 하위 컴포넌트에 전달할 상위 컴포넌트의 data 속성을 지정한다. 
```
<div id="app">
	<child-component v-bind:propsdata="message"></child-component>
</div>
<script type="text/javascript">
	Vue.component('child-component', {
		props : ['propsdata'],
	var vw = new Vue({
		template : '<p>{{propsdata}}</p>'
	})
		el: '#app',
		data: {
			message: 'Hello Vue! passed from parent component'
		}
	})
</script>
```

> ※ example : 04_component_communication1.html

#### 하위에서 상위 컴포넌트(인스턴스)로 이벤트 전달
하위 컴포넌트에서 상위 컴포넌트로 신호를 보내서 상위 컴포넌트의 메소드를 실행할 수도 있고, 응용하여 하위 컴포넌트로 내려보내는 props의 값을 조정할 수도 있다. 공식 사이트의 이벤트 발생 사용 방법에서는 하위에서 상위로 데이터를 전달하는 방법을 다루지 않는지만(단방향 데이터 흐름에 어긋나는 구현 방법임), 향후 복잡한 애플리케이션을 구축할 때 필요한 경우가 종종 있다.

```
<div id="app">
	<child-component v-on:show-log="printText"></child-component>
</div>
<script type="text/javascript">
	Vue.component('child-component', {
		template: '<button type="button" v-on:click="showLog">show</button>',
		methods: { 
			showLog: function() {
				this.$emit('show-log');
			}
		}
	})
	var vw = new Vue({
		el: '#app',
		data: {
			message: 'Hello Vue! passed from parent component'
		},
		methods: {
			printText: function() {
				console.log('received an event');
			}
		}
	})
</script>
```

> ※ example : 04_component_communication2.html

#### 같은 레벨 컴포넌트간의 통신
뷰는 상위에서 하위로만 데이터를 전달해야 하는 기본적인 통신 규칙을 따르기 때문에 형제 컴포넌트끼리 값을 전달 하려면 공통 상위 컴포넌트로 이벤트를 전달한 후 공통 상위 컴포넌트에서 2개의 하위 컴포넌트에 props를 내려 보내야 한지만 이벤트 버스(Event Bus)를 사용하여 상위 컴포넌트 없이 통신할수 있는 방법도 존재한다.
이벤트 버스를 구현하려면 애플리케이션 로직을 담는 인스턴스와는 별개로 새로운 인스턴스 하나를 더 생성하고, 새 인스턴스를 이용하여 보내고 받아야 한다. 보내는 컴포넌트에서는 .$emit()을, 받는 컴포넌트에서는 .$on()을 구현한다. 이벤트버스를 사용하면 props 속성을 이용하지 않고도 원하는 컴포넌트간에 직접적으로 데이터를 전달할수 있어 편리하지만, 컴포넌트가 많아지면 관리가 되지않는 이슈가 있다. 이 문제를 해결하려면 뷰엑스(Vuex)라는 상태 관리 도구가 필요하지만 여기서는 다루지 않도록 한다.

```
<div id="app">
	<!-- 같은 레벨의 컴포넌트로 데이터 전달 -->
	<child-component></child-component>
</div>
<script type="text/javascript">
	var eventBus = new Vue();

	Vue.component('child-component', { 
		template: '<div>하위 컴포넌트 영역입니다.<button type="button" v-on:click="showLog">show</button></div>',
		methods: {
			showLog: function() {
				eventBus.$emit('triggerEventBus', 100);
			}
		}
	})

	var vw = new Vue({
		el: '#app',
		created: function(){
			eventBus.$on('triggerEventBus', function(value) {
				console.log('이벤트를 전달 받음. 전달받은 값 :', value);
			});
		}
	})
</script>
```

> ※ example : 04_component_communication3.html

## 뷰 라우터
뷰 라우터는 뷰에서 라우팅 기능을 구현할 수 있도록 지원하는 공식 라이브러리이다. 뷰 라우터를 이용하여 뷰로 만든 페이지 간에 자유롭게 이동할 수 있다.

### 라우팅(Roution)
라우팅이란 웹 페이지 간의 이동 방법을 말한다. 라우팅은 현대 웹 앱 형태 중 하나인 싱글 페이지 애플리케이션(SPA, Single Page Application)에서 주로 서용 된다.
라우팅을 이용하면 화면간의 전환이 매끄럽고 애플리케이션의 사용자 경험을 향상시킬 수 있다. 일반적으로 브라우저에서 웹 페이지를 요청하면 응답시간 동안 깜빡거리는 현상이 나타나는데, 라우팅으로 처리하면 화면을 매끄럽게 전환 할 수 있을 뿐 아니라 더 빠르게 화면 조작이 가능하다.


- &lt;router-link to="url"&gt; : 페이지로이동 태그, 화면에서는 <a>로 표시되며 클릭하면 지정한 URL로 이동
- &lt;router-view&gt; : 페이지 표시 태그. 변경되는 URL에 따라 해당 컴포넌트를 뿌려주는 영역

```
<div id="app">
	<p>
		<router-link to="/main">Main 컴포넌트로 이동</router-link> <!-- URL 값을 변경하는 태그 -->
		<router-link to="/login">Login 컴포넌트로 이동</router-link> <!-- URL 값을 변경하는 태그 -->
	</p>
	<router-view></router-view> <!-- URL 값에 따라 갱신되는 화면 -->
</div>
<script type="text/javascript">
	var Main = { // main 컴보넌트 정의
		template: '<div>main</div>'
	}
	var Login = { // login 컴포넌트 정의
		template: '<div>login</div>'
	}

	var routes = [ // 각 URL에 맞춰 표시할 컴포넌트 지정
		{
			path: '/main', 
			component: Main
		},
		{
			path: '/login', 
			component: Login
		}
	]

	var router = new VueRouter({ // 뷰 라우터 정의
		routes
	})

	var vw = new Vue({ // 뷰 인스턴스에 라우터 추가
		router
	}).$mount('#app');
</script>
```
> ※ example : 05_router.html

#### $mount() API란?
해당 값은 el 속성과 동일하게 인스턴스를 화면에 붙이는 역할을 한다. 인스턴스를 생성할 때 el 속성을 넣지 않았더라도 생성하고 나서 $mount()를 이용하면 강제로 인스턴스를 화면에 붙일 수가 있다. 참고로 뷰 라우터의 공식 문서는 모두 인스턴스 안에 el를 지정하지 않고 해당 방법을 사용하여 안내하고 있다.

#### 라우터 URL 해시 값(#) 삭제법
```
var router = new VueRouter({
	mode: 'history',
	routes
})
```

### 네스티드 라우터(Nested Router)
네스티드 라우터는 라우터로 페이지를 이동할 때 최소 2개 이상의 컴포넌트를 화면에 나타낼 수 있다. 상위 컴포넌트 1개에 하위 컴포넌트 1개를 포함하는 구조로 구성된다.
네스티드 라우터를 이용하면 URL에 따라 컴포넌트의 하위 컴포넌트가 다르게 표시된다.



## 디렉티브

