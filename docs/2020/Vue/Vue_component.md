# Vue.js 컴포넌트
***

#### Vue 컴포넌트란?
Vue 컴포넌트(Component)란 조합하여 화면을 구성할 수 있는 블록(화면 특정 영역)을 의미합니다. 컴포넌트를 활용하면 화면을 빠르게 구조화하여 일괄적인 패턴으로 개발할 수 있습니다. 화면 영역을 컴포넌트로 쪼개서 재활용할 수 있는 형태로 관리하면 나중에 코드를 다시 사용하기가 훨씬 편리하고 정해진 방식대로 컴포넌트를 등록하거나 사용하므로 남이 작성한 코드를 직관적으로 이해가 가능합니다.

***
#### Vue 컴포넌트 등록하기
Vue 컴포넌트 등록 방법은 전역과 지역 두가지 방법이 있습니다. 지역(Local)컴포넌트는 특정 인스턴스에서만 유효한 범위를 갖고, 전역(Global)컴포넌트는 여러 인스턴스에서 공통으로 사용할 수 있습니다. 즉 지역(Local)은 특정 범위 내에서만 사용할 수 있고, 전역(Global)은 Vue로 접근 가능한 모든 범위에서 사용이 가능합니다.

- 전역(Global) Component : 여러 인스턴스에서 공통으로 사용할 수 있는 컴포넌트
- 지역(Local) Component : 특정 인스턴스에만 유효한 범위를 갖음

***
#### 1. 전역(Global) 컴포넌트 등록
전역 컴포넌트는 라이브러리 로딩후 Vue 변수를 이용하여 등록합니다.

```javascript
Vue.Component("컴포넌트이름",{
    // 컴포넌트 내용
});
```
- 컴포넌트 이름 : template 속성에서 사용할 HTML사용자 정의 태그(custom tag)
- 컴포넌트 내용 : 컴포넌트 태그가 실제 화면의 HTML요소로 변활할 때 표시될 속성들을 **컴포넌트 내용**에 작성 (template, data, methods 등 인스턴스 옵션 속성을 정의할 수 있습니다.)

👇 입력
```javascript
<div id="app">
    <my-component></my-component> <!-- 전역 컴포넌트 표시 -->
</div>
<script>
    Vue.component('my-component',{ // 컴포넌트이름
        template: "<div>전역 컴포넌트 등록</div>" // 컴포넌트 내용
    });

    new Vue({
        el: '#app'
    })
</script>
```
👇 결과
```javascript
<div id="app">
    <div>전역 컴포넌트 등록</div> <!-- 등록한 my-component가 변환된 모습 -->
</div>
```
***
#### 2. 로컬(Local) 컴포넌트 등록
인스턴스에 components 속성을 추가하고 등록할 컴포넌트 이름과 내용을 정의 합니다.
```javascript
new Vue({
    components: {
        '컴포넌트 이름' : 컴포넌트 내용
    }
});
```
- 컴포넌트 이름 : 전역 컴포넌트와 마찬가지로 HTML에 등록할 사용자 정의태그를 의미합니다.
- 컴포넌트 내용 : 컴포넌트 태그가 실제화면 요소로 변환될 때의 내용을 의미합니다.

👇 입력
```javascript
<div id="app">
    <my-component></my-component> <!-- 로컬 컴포넌트 표시 -->
</div>
<script>
    var cmp = {
        template: '<div>지역 컴포넌트 등록</div>' // 화면에 보여질 컴포넌트 내용 정의
    };

    new Vue({
        el: '#app',
        components: {
            'my-component' : cmp // '컴포넌트 이름' : 컴포넌트 내용
        }
    })
</script>
```
👇 결과
```javascript
<div id="app">
    <div>지역 컴포넌트 등록</div> <!-- 등록한 my-component가 변환된 모습 -->
</div>
```
***
#### 3. 전역, 지역 컴포넌트 차이
```javascript
<div id="app">
    <my-global-component></my-global-component>
    <my-local-component></my-local-component>
</div>
<div id="app2">
    <my-global-component></my-global-component>
    <my-local-component></my-local-component>
</div>
<script>
    Vue.component("my-global-component", {
        template : "<div>전역 컴포넌트가 등록되었습니다.</div>"
    });
    var cmp = {
        template : "<div>지역 컴포넌트가 등록되었습니다.</div>"
    };

    new Vue({
        el : "#app",
        components : {
            "my-local-component" : cmp
        }
    });

    new Vue({
        el : "#app2",

    })
</script>
```
👇 결과
```javascript
<div id="app">
    <div>전역 컴포넌트가 등록되었습니다.</div>
    <div>지역 컴포넌트가 등록되었습니다.</div>
</div>
<div id="app2">
    <div>전역 컴포넌트가 등록되었습니다.</div>
</div>
```
전역 컴포넌트와 지역 컴포넌트의 유효 범위가 다르기 때문에 첫번째 영역(#app)에서는 전역,지역 컴포넌트가 나타나고 두번째 영역(#app2)에서는 전역 컴포넌트만 나타납니다.

1. 전역 컴포넌트는 인스턴스를 새로 생성 할때마다 인스턴스에 components 속성으로 등록할 필요없이 한 번 등록하면 어느 인스턴스에서 사용이 가능합니다.
2. 지역 컴포넌트는 새 인스턴스를 생성할 때마다 등록해줘야 합니다.
  

***
##### 참고자료
https://ux.stories.pe.kr/131<br>

소중한 자료 감사합니다 😀
***

