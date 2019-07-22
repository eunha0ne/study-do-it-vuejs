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

## 화면을 개발하기 위한 필수 단위
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

|<router-link to="URL 값">|페이지 이동 태그 화면에서 <a> 테그로 표현되고, to에 지정한 URL로 이동|
|<router-view>|페이지 표시 태그, 변경되는 URL에 따라 해당 컴포넌트를 뿌려주는 영역|

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
