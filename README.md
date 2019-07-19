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
  * beforeCreate
  * created
  * beforeMount
  * mounted
  * beforeUpdate
  * updated
  * beforeDestory
  * destroyed

### 컴포넌트
* 재사용이 가능하도록한 화면 구성의 최소 단위
* 전역 컴포넌트와 지역 컴포넌트는 유효 범위가 다르다.

### 뷰 컴포넌트 통신
* props 전달은 v-bind 속성을 사용
```html
<child-component v-bind:props 속성 이름="상위 컴포넌트의 data 속성"></child-component>
```

### 하위에서 상위 컴포넌트로 이벤트 전달하기
```javascript
// 이벤트 발생
this.$emit('이벤트명');
```

```html
// 이벤트 수신
<child-component v-on:이벤트명="상위 컴포넌트의 메서드 명"></child-component>
```
