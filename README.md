[English](https://github.com/ShowPenZ/vue-ripple-button/blob/master/README_en-US.md) | 中文

# vue-ripple-button

> 一个带波纹效果的vue按钮组件

## Installation

```
$ npm install vue-ripple-button --save
$ yarn add vue-ripple-button
```

## Usage


``` vue
<script>
import RippleBtn from "vue-ripple-button";

export default {
  name: "RippleBtn",
  data() {
    return {};
  },
  methods: {},
  render() {
    const onClick = () => {
      console.log(23523);
    };

    return (
      <div class="container">
        <RippleBtn text="1312312311" {...{ on: { onclick: onClick } }} />
      </div>
    );
  }
};
</script>
<style>
</style>
```
# License

MIT
