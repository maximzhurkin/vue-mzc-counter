# vue-mzc-counter
Simple Vue2 counter component

![](demo.gif)

[Online demo](https://codesandbox.io/s/competent-dhawan-exec2?file=/src/App.vue)

## Installation
```sh
npm install vue-mzc-counter --save
```

## Usage
```js
import VueMzcCounter from "vue-mzc-counter";
import "vue-mzc-counter/src/vue-mzc-counter.css";

export default {
  components: {
    VueMzcCounter,
  },
  methods: {
    changeCounter(count) {
      console.log(count);
    }
  },
};
```
```html
<vue-mzc-counter :value="2" :max="12" unit="шт" @change="changeCounter" />
```