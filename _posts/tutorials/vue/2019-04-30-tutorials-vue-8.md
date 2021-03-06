---
layout: post
title: 'state, this'
categories: [Tutorials]
image: assets/images/tutorials/common/vue_bg.png
tag: [Vue.js, javascript]
---

> ## state관리와 this

Vue에서 state는 data입니다.

```javascript
var App = new Vue({
  el: '#app',
  data: {
    // 이 부분이 state이자 data
  },
})
```

Vue의 data는 변수처럼 변경이 가능합니다.

```javascript
var App = new Vue({
  el: '#app',
  data: {
    model: 'Vue.js', // model -> 'Vue.js'
  },
  created() {
    this.model = 'Hello Vue.js' // model -> 'Hello Vue.js'
  },
  mounted() {
    this.model = 'Change Vue.js' // model -> 'Change Vue.js'
  },
})
```

data들을 this를 이용해서 불러오고 변수처럼 수정을 할 수 있습니다.

Vue에서 this는 Vue인스턴스를 바라보는데 즉 new Vue를 가리키고 있습니다.

그러면 이거를 이용해서 조금 더 재미있는 결과를 얻을 수 있습니다.

```css
* {
  margin: 0;
  padding: 0;
}

#app {
  width: 300px;
  margin: 20px auto;
}
h1 {
  text-align: center;
  font-size: 20px;
  margin-bottom: 20px;
  border-bottom: 2px solid #000;
}
p {
  font-size: 15px;
  margin-bottom: 10px;
  border-bottom: 1px solid #9f9f9f;
}
a {
  display: block;
  width: 60px;
  height: 30px;
  line-height: 30px;
  margin: 0 auto;
  text-align: center;
  border: 1ox solid #000;
  border-radius: 10px;
}
```

```html
<div id="app">
  <h1>{% raw %}{{ title }}{% endraw %}</h1>
  <p v-if="show">내가 보이나요?</p>
  <a href="#" @click.prevent="changeDate()">Click!</a>
</div>
```

우선 html을 작성해서 모양을 잡았습니다.

스크립트를 추가하는데 data는 총 두개가 들어갈 예정입니다.

```javascript
var App = new Vue({
  el: '#app',
  data: {
    title: 'Instance 생성',
    show: false,
  },
  methods: {
    changeDate() {},
  },
})
```

결과를 확인해보겠습니다.

![결과 이미지 1]({{ site.baseurl }}/assets/images/tutorials/vue/8/img1.jpg)

스크립트 부분만 추가하겠습니다.

```javascript
var App = new Vue({
  el: '#app',
  data: {
    title: 'Instance 생성',
    show: false,
  },
  updated() {
    this.title = 'Data 업데이트!!!!'
  },
  methods: {
    changeDate() {
      this.show = true
    },
  },
})
```

methods안에 있는 changeDate()가 실행이 되면서 `this.show = true`부분을 통해서 show가 true가 됬었습니다.

그리고 data가 업데이트 되었으니 updated가 실행되고 `this.title = 'Data 업데이트!!!!'`를 통해서 title이 바뀌었습니다.
