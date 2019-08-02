# Do it Vue.js
  
## Vue.js란?
* 화면을 개발을 위한 Progresiive framework(점진적인 프레임워크), 라이브러리의 역할도 수행할 수 있다.
  * 프레임워크
    * 개발 생산성을 높이기 위해서 일정한 틀과 규칙에 따라 개발하도록 미루 구조를 정의해 놓은 도구
  * 라이브러리
    * 자주 사용되는 기능을 모아 재활용할 수 있도록 정리한 기술 모음집
* 프레임워크의 기능인 라우터, 상태관리, 테스팅을 쉽게 결합할 수 있음
  
### 뷰의 특징
* 앵귤러의 데이터 바인딩 특성
  * (Two-way Data Binding)양방향 데이터 바인딩 + 리액트의 (One-way Data Flow)단방향 데이터 흐름의 장점을 결합함
* 리액트의 Virtual DOM(가상 돔) 기반 렌더링
* UI 화면단 라이브러리
  * 개발 방법론 중 MVVM(Model - View - ViewModel) 패턴의 ViewModel(뷰 모델)에 해당하는 화면단 라이브러리이다.
    * 마크업 언어나 GUI 코드를 비즈니스 로직 또는 벡엔드 로직과 분리하여 개발하는 소프트웨어 디자인 패턴
* 컴포넌트 기반 프레임워크
  * 코드의 재사용성이 좋음
  
  
## 개발 환경 설정
### 뷰 개발자 도구 설치하기
* [Vue.js devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd/related)
  * 크롬 > `...` 설정 > 도구 더보기 > 확장 프로그램 > Vue.js devtools > 파일 URL에 대한 액세스 허용
  
## 뷰 프론트 개발
### 인스턴스
```javascript
// 뷰 인스턴스
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  }
});
```
* 뷰 인스턴스를 생성하면 HTML의 특정 범위 안에서만 옵션 속성들이 적용되어 나타난다. 이를 `인스턴스의 유효 범위`라고 함.
* 인스턴스 생성시 화면에 인스턴스 옵션 속성을 적용하는 과정
  * 뷰 라이브러리 파일 로딩
  * 인스턴스 객채 생성 (옵션 속성 포함)
  * 특정 화면 요소에 인스턴스를 붙임
  * 인스턴스 내용이 화면 요소로 변환
  * 변환된 화면 요소를 사용자가 최종 확인
* 뷰 인스턴스 라이프 사이클 속성
  * beforeCreate -> created -> beforeMount -> mounted -> beforeUpdate -> updated -> beforeDestory -> destroyed

### 컴포넌트
* 재사용이 가능하도록한 화면 구성의 최소 단위
* 전역 컴포넌트와 지역 컴포넌트의 유효 범위가 다르다.

### 뷰 컴포넌트 통신
#### 상위에서 하위 컴포넌트로 데이터 전달하기
* props 전달은 v-bind 속성을 사용
```html
<!-- 상위 컴포넌트의 HTML 코드 -->
<child-component v-bind:props 속성 이름="상위 컴포넌트의 data 속성"></child-component>
```

```javascript
// 하위 컴포넌트의 props 속성 정의 방식
Vue.component('child-component', {
  props: ['props 속성 이름']
});
```

#### 하위에서 상위 컴포넌트로 이벤트 전달하기
* 이벤트 발생과 수신 형식
```javascript
// 이벤트 발생
this.$emit('이벤트명');
```

```html
<!-- 이벤트 수신 -->
<child-component v-on:이벤트명="상위 컴포넌트의 메서드 명"></child-component>
```

* 이벤트 버스 형식
앱 로직을 담는 뷰 인스턴스와는 별개의 새로운 인스턴스 1개를 더 생성하고, 그렇게 생성한 새 인스턴스를 사용해서 이벤트를 보내고 받는다. 보내는 쪽에서는 `$emit()`을 사용, 받는 컴포넌트는 `$on()`
```javascript
var eventBus = new Vue();

// 이벤트를 보내는 컴포넌트는
...
methods: {
  메서드명: function () {
    eventBus.$emit('이벤트명', 데이터);
  }
}

// 이벤트를 받는 컴포넌트는
...
methods: {
  created: function () {
    eventBus.$on('이벤트명', function (데이터) {
      ...
    });
  }
}
```

## 상용 웹 앱을 개발하기 위한 필수 기술들
### 뷰 라우터
* 라우팅이란?
  * 라우팅이란 웹 페이지 간의 이동 방법을 말함.
  * 라우팅은 모던 웹 형태 중 하나인 SPA, Single Page Application(싱글 페이지 애플리케이션)에서 주로 사용하고 있음

* 라우팅의 이점
  * 화면 간의 전환이 매끄럽다.
  * 사용자 경험을 향상시킬 수 있다.

* 뷰 라우터
  * 뷰에서 라우팅 기능을 구현할 수 있도록 지원하는 공식 라이브러리

|태그|설명|
|---|---|
| `<router-link to="URL 값">` | 페이지 이동 태그 화면에서 `<a>` 테그로 표현되고, to에 지정한 URL로 이동 |
| `<router-view>` | 페이지 표시 태그, 변경되는 URL에 따라 해당 컴포넌트를 뿌려주는 영역 |

### 네스티드 라우터
* 부모 컴포넌트 내용을 정의한 상태에서 URL에 따라서 하위 컴포넌트를 다르게 그릴 수 있음
```javascript
    // feature/exam-04-1

    // 컴포넌트 정의
    // <router-view> 부분은 하위 컴포넌트를 리턴할 영역
    var User = {
      template: `
      <div>
        User Component
        <router-view>
      </div>
      `
    };
    var UserProfile = { template: '<p>User Profile Component</p>' };
    var UserPost = { template: '<p>User Post Component</p>' };

    // 네스티드 라우팅 정의
    var routes = [
      {
        path: '/user',
        component: User,
        children: [
          {
            path: 'posts',
            component: UserPost
          },
          {
            path: 'profile',
            component: UserProfile
          }
        ]
      }
    ];

    // 라우터 정의
    var router = new VueRouter({
      routes
    });

    // 뷰 인스턴스에 라우터 추가
    new Vue({
      router
    }).$mount('#app');

    // 실행 결과 확인해 보기
    // index.html#/user
    // index.html#/user/posts
```

### 네임드 뷰
* 특정 페이지로 이동했을 때 여러 개의 컴포넌트를 동시에 표시하는 라우팅 방식
  * `네스티드 라우터`는 상위 컴포넌트가, 하위 컴포넌트를 포함
  * `네임드뷰`는 같은 레벨에서 여러 개의 컴포넌트를 한 번에 표시

```javascript
// 컴포넌트 정의
var Body = { template: '<div>This is Body</div>' };
var Header = { template: '<div>This is Header</div>' };
var Footer = { template: '<div>This is Footer</div>' };

// 라우터 정의
var router = new VueRouter({
  routes: [
    {
      path: '/',
      components: {
        default: Body,
        header: Header,
        footer: Footer
      }
    }
  ]
});

// 뷰 인스턴스에 라우터 추가
var app = new Vue({
  router
}).$mount('#app');
```

### 뷰 HTTP 통신
#### 뷰 리소스 (depricated) 

> 더이상 지원하지 않는다고 함, 레거시 코드를 대비해서 참고해 두기

```javascript
...
methods: {
  getData: function () {
    this.$http.get('https://raw.githubusercontent.com/joshua1988/doit-vuejs/master/data/demo.json')
      .then(function (response) {
        console.log(response);
        console.log(JSON.parse(response.data));
      });
  }
}
```

#### [Axios](https://www.npmjs.com/package/axios)
* 설치
  * CDN
  ```javascript
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  ```
  * npm
  ```
  $ npm install axios
  ```

|API 유형|처리 결과|
|---|---|
|axios.get('URL 주소').then().catch()|HTTP GET|
|axios.post('URL 주소').then().catch()|HTTP POST|
|axios({ 옵션 속성 })|HTTP 요청에 대한 자세한 속성을 직접 정의|

```javascript
...
methods: {
  getData: function () {
    axios.get('https://raw.githubusercontent.com/joshua1988/doit-vuejs/master/data/demo.json')
      .then(function (response) {
        console.log(response);
        console.log(response.data);
      });
  }
```

## 템플릿
* 뷰 Template(탬플릿)이란?
  * HTML, CSS, 등의 마크업 속성과 뷰 인스턴스에서 정의한 데이터 및 로직을 연결하여 화면을 HTML로 변환하여 구성해 주는 속성
  ```javascript
  new Vue({
    template: '<p>{{ message }}</p>'
  });
  ```

템플릿에서 사용하는 뷰의 속성과 문법
<br>
1. 데이터 바인딩
2. 자바스크립트 표현식
3. 디렉티브
4. 이벤트 처리
5. 고급 템플릿 기법

### 1. 데이터 바인딩
#### {{ }}
```html
<div id="app">
  {{ message }}
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: 'Hello Vue.js'
    }
  });
</script>
```
    
뷰 데이터가 변경되어도 값을 바꾸고 싶지 않은 경우에는 `v-once` 속성을 사용
```html
<div id="app" v-once>
  {{ message }}
</div>
```

#### v-bind
아이디, 클레스, 스타일 등의 HTML 속성값에 뷰 데이터 값을 연결할 때 사용하는 데이터 연결 방식으로 HTML 속성이나 props 속성 앞에 접두사로 붙여줌
```html
<div id="app">
  <p v-bind:id="someId">아이디 바인딩</p>
  <p v-bind:class="someClass">클레스 바인딩</p>
  <p v-bind:style="someStyle">스타일 바인딩</p>

  <!-- 축약 포현 -->
  <p :id="someId">아이디 바인딩</p>
  <p :class="someClass">클레스 바인딩</p>
  <p :style="someStyle">스타일 바인딩</p>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      someId: 10,
      someClass: 'container',
      styleA: 'color: blue'
    }
  });
</script>
```

### 2. 자바스크립트 표현식
{{ }} 안에 자바스크립트 표현식을 사용할 수 있음. 단, 선언문과 분기 구문은 사용할 수 없음. 화면에는 간단한 연산 결과만 표시하고, 복잡한 연산은 인스턴스 안에서 처리
```html
<div id="app">
  {{ !isReverse && reverseMessage }}
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      isReverse: false,
      message: 'Hello Vue.js'
    },
    // 데이터 속성을 계산해 주는 속성
    computed: { 
      reverseMessage: function () {
        return this.message.split('').reverse().join('');
      }
    }
  });
</script>
```


### 3. 디렉티브
뷰 Directive(디렉티브)란 HTML 태그 안에 v- 접두사를 가지는 모든 속성을 의미. v-bind 또한 디렉티브에 해당
  
``` html
<a v-if="flag">Vue.js</a>
```

|디렉티브 이름|역할|
|------|---|
|v-if|지정한 불리언 값으로 HTML 태그를 렌더링|
|v-for|지정한 뷰 데이터의 개수만큼 반복 출력|
|v-show|지정한 불리언 값으로 CSS display 속성에 영향|
|v-bind|HTML 속성과 뷰 데이터 속성을 binding(연결)|
|v-on|이벤트를 감지할 때 사용. v-on:click는 클릭 이벤트 감지하여 특정 메서드를 실행하게 할 수 있음|
|v-model|폼에서 주로 사용하는 속성. 입력한 값이 뷰 인스턴스 데이터와 즉시 동기화됨. 입력된 값을 서버로 보내거나, watch와 같은 고급 속성을 이용해서 추가 로직을 수행할 수 있음. 단, `input, select, textarea` 태그에서만 사용 가능|


### 4. 이벤트 처리
이벤트 처리를 위해서 `v-on` 디렉티브와 methods 속성을 활용함
```html
<button v-on:click="clickBtn">클릭</button>

<script>
  ...
  methods: {
    clickBtn: function () {
      alert('clicked');
    }
  }
</script>
```
### 5. 고급 템플릿 기법
#### computed
data 속성 값의 변화에 따라 자동으로 다시 연산한다. 그리고 연산된 값은 캐싱을 통해서 필요할 때 불러온다. 
#### computed와 methods 차이
methods 속성은 호출할 떄만 해당 로직이 수행되고, computed 속성은 대상 데이터의 값이 변경되면 자동적으로 수행된다는 차이가 있음. 따라서 복잡한 연산을 반복 수행해야 된다면 computed 속성이 성능 면에서 효율적임
#### watch
데이터 변화를 감지하여 특정 로직을 수행. 데이터 호출과 같이 시간이 상대적으로 더 많이 소모되는 비동기 처리에 적합
```html
<div id="app">
  <input v-model="message">
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  },
  watch: {
    message: function (data) {
      console.log("message의 값이 변경:", data);
    }
  }
})
</script>
```
인풋 박스의 입력 값을 디렉티브로 바인딩하고 입력 값에 변화를 감지해서 로직을 수행

## 중·고급 기술을 위한 배경 지식
* Vuex
  * 상태 관리 라이브러리
* Vue Reactivity
  * 뷰가 데이터 변화를 감지하고 자동으로 화면을 갱신하는 특성
* Server Side Rendering: SSR
  * 서버 사이드 렌더링

### Vuex
* Vue.js 상태 관리 라이브러리: [뷰엑스](vuex.vuejs.org/en/intro.html)
* 애플리케이션에서 사용하는 데이터를 중앙에서 효율적으로 관리하는 것  

### Vue Reactivity(뷰 반응성)
데이터 변화를 감지했을 때 자동으로 화면을 다시 갱신하는 특성. 뷰 인스턴스가 생성될 때 data 속성에 정의된 객체들은 특정한 변환 작업을 거치면서 라이브러리에서 정의된 모든 속성을 getter와 setter의 형태로 변환되어서 내부적으로 사용됨.

화면을 갱신하는 속성 watcher(이하, 왓쳐)는 모든 컴포넌트에 존재하는 속성으로 화면을 그리는데 중요한 역할을 함. 인스턴스가 그려지고 나서, 데이터 속성을 바꾸거나 접근하면 왓쳐에서 해당 사실을 감지하고 렌더링.

인스턴스 데이터 속성에 반응성이 생성되는 순간은 인스턴스를 생성하는 시점이기 때문에 인스턴스 생성 이후에 데이터 속성에 객체를 추가하면 그 객체에는 반응성이 생기지 않음.

* [뷰 반응성](http://vuejs.org/v2/guide/reactivity.html)

### 서버 사이트 렌더링
* 클라이언트 사이드 렌더링은 웹 페이지를 화면에 그릴 때 화면을 그리는 동작을 클라이언트에서 수행하는 것을 의미. 다 그려져 있지 않은 HTML 페이지를 브라우저에서 받고 자바스크립트를 이용해서 나머지 부분을 그리는 것을 의미. 장점은 매끄러운 화면 전환과 사용자 경험의 향상.
* 서버 사이드 렌더링은 완벽히 그려진 HTML 페이지를 브라우저에서 받는 것을 의미. 강점은 검색 엔진 최적화(SEO, Search Engine Optimiziation)와 초기 화면 렌더링 속도. 다 그려져 있는 상태에서 화면에 단순히 나타내기만 하는 것과 자바스크립트 라이브러리를 로딩하고 데이터와 화면 요소를 계싼하여 화면에 나타내는 것은 속도에서 차이가 있음.
* [Nuxt.js](http://nuxtjs.org/)

### 웹팩


## 참고 링크
* [Vue Media Query](https://alligator.io/vuejs/vue-media-queries/)