# study-do-it-vuejs

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
