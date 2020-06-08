# Vue.js 인스턴스
---

#### Vue 인스턴스란?
- Vue 인스턴스란 생성된 Vue 오브젝트를 말한다.
- Vue 를 실행하기 위해 첫번째로 정의하고 생성해야 하는 객체.

***
#### Vue 인스턴스 생성
Vue 생성자로 인스턴스를 만드는 방법은 아래와 같다. <br>
Vue 인스턴스를 참조하기 위해 변수 **vm(ViewModel의 약자)**을 종종사용
```javascript
var vm = new Vue({
    el: '#app', // 인스턴스가 뿌려질 지점
    template: '', // 인스턴스의 화면 내용
    data: {}, // 인스턴스가 갖는 데이터
    props: [], // {}
    methods: {}, // 인스턴스의 이벤트 정의
    computed: {},
    wath: {}
})
```
<strong>Vue 인스턴스 옵션 속성</strong>
- el : Vue가 실행될 HTML의 DOM요소를 지정
- template : 화면에 표시할 HTML, CSS 등의 마크업 요소를 정의하는 속성
- data : Vue의 반응성이 반영될 데이터
- props : 부모 컴포넌트로부터 전달 받은 property들의 array 또는 Object
- methods : 함수를 정의하고 화면의 동작과 이벤트를 정의하는 메소드
- computed : data의 값이 변화되었을 때 수행할 메소드 정의
- watch : 지정된 변수를 지켜보고 있다가 값이 변경되었을때 정의된 함수를 호출

***
#### Vue 라이프사이클
- 라이프사이클은 Vue 인스턴스의 생성부터 파괴까지의 일련의 과정을 말합니다.
- 생성(Create) > 초기화(Mount) > 갱신(Update) > 소멸(Destroy)
- 사용자는 Vue 인스턴스를 생성할 때 라이프사이클 훅(hook)을 정의할 수 있습니다.

<br>

![라이프사이클](img/img_vue_lifecycle.png)

<strong>1. beforeCreate</strong>
<p>
    인스턴스가 생성되고 나서 가장 처음으로 실행되는 라이프 사이클 단계입니다. 이 단계에서는 data속성과 methodes 속성이 아직 인스턴스에 정의되어 있지 않고, 돔과 같은 화면 요소에도 접근할 수 없습니다.
</p>
<strong>2. created</strong>
<p>
    data 속성과 methods 속성이 정의 되었기 때문에 this.data 또는 this.fetchData()와 같은 로직들을 이용하여 data 속성과 methods 속성에 정의 된 값에 접근하여 로직을 실행할 수 있습니다. 다만, 아직 인스턴스가 화면 요소에 부착되기 전이기 때문에 template 속성에 정의된 돔 요소로 접근할 수 없습니다.
</p>
<strong>3. beforeMount</strong>
<p>
    created 단계 이후 template 속성에 지정한 마크업 속성을 render() 함수로 변환 후 el 속성에 지정한 화면 요소(돔)에 인스턴스를 부착하기 전에 호출되는 단계입니다. render()함수가 호출되기 직전의 로직을 추가하기 좋습니다.
</p>
<strong>4. mounted</strong>
<p>
    el속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 호출되는 단계로, template 속성에 정의한 화면 요소에 접근할 수 있어 화면 요소를 제어하는 로직을 수행하기 좋은 단계입니다. 다만 돔에 인스턴스가 부착되자마자 바로 호출되기 때문에 하위 컴포넌트나 외부 라이브러리에 의해 추가된 화면 요소들이 최종 HTML 코드로 변환되는 시점과 다를 수 있습니다.
</p>
<strong>5. beforeUpdate</strong>
<p>
    el 속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 인스턴스에 정의한 속성들이 화면에 치환됩니다. 치환 된 값은 뷰의 반응성을 제공하기 위해 $watch 속성으로 감시합니다. 이를 데이터 관찰이라고 합니다.
</p>
<strong>6. updated</strong>
<p>
    데이터가 변경되고 나서 가상 돔으로 다시 화면을 그리고 나면 실행되는 단계입니다. 데이터 변경으로 인한 화면 요소 변경까지 완료된 시점으로 데이터 변경 후 화면 요소 제어와 관련된 로직을 추가하기 좋은 단계입니다.이 단계에서 데이터 값을 변경하면 무한 루프에 빠질 수 있기 때문에 값을 변경하려면 computed, watch와 같은 속성을 사용해야 합니다. 가급적이면 beforeUpdate에 추가하고 updated에서는 변경 데이터의 화면 요소와 관련된 로직을 추가하는 것이 좋습니다.
</p>

<strong>7. beforeDestroy</strong>
<p>
    Vue 인스턴스가 파괴되기 직전에 호출되는 단계입니다. 이 단계에서는 아직 인스턴스에 접근할 수 있습니다. 따라서 Vue 인스턴스의 데이터를 삭제하기 좋은 단계입니다.
</p>

<strong>8. destroyed</strong>
<p>
    Vue 인스턴스가 파괴되고 나서 호출되는 단계입니다. Vue 인스턴스에 정의한 모든 속성이 제거되고 하위에 선언한 인스턴스들 또한 모두 파괴됩니다.
</p>

***
#### Vue 라이프사이클 훅
라이프 사이클 훅은 인스턴스의 특정 시점에 원하는 로직을 구현할 수 있습니다. 예를 들어, 컴포넌트가 생성되자마자 데이터를 서버에서 받아오고 싶으면 created나 beforeMount 라이프사이클 훅을 사용할 수 있습니다. 아래 코드는 인스턴스가 생성되자마자 엑시오스로 HTTP GET 요청을 보내 데이터를 받아오는 코드입니다.
```javascript
new Vue({
    methods: {
        fetchData(){
            axios.get(url);
        }
    },
    created: function(){
        this.fetchData();
    }
})

```

***
##### 참고자료
https://velog.io/@psm8873/2019.01.12-Vue-인스턴스-7mjqyi53cl<br>
https://ux.stories.pe.kr/113<br>

소중한 자료 감사합니다 😀
***

