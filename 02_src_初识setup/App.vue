<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <button @click="sayHello">说话</button>
</template>

<script>
/*  
  尽量不要与Vue2.x配置混用
    - Vue2.x配置（data、methos、computed...）中<strong style="color:#DD5145">可以访问到</strong>setup中的属性、方法。
    - 但在setup中<strong style="color:#DD5145">不能访问到</strong>Vue2.x配置（data、methos、computed...）。
    - 如果有重名, 根据配置项顺序，后配置的数据覆盖前配置的数据。
  setup不能是一个async函数，因为返回值不再是return的对象, 而是promise, 模板看不到return对象中的属性。（后期也可以返回一个Promise实例，但需要Suspense和异步组件的配合）
*/

// import { h } from 'vue'
export default {
  name: 'App',
  // 当vue2和vue3中数据重名，配置在后的覆盖配置在前的数据
  data() {
    return {
      name: '李四'
    }
  },
  // 此处只是测试一下setup，暂时不考虑响应式的问题
  setup() {
    // 数据
    let name = '张三'
    let age = 16

    // 方法
    function sayHello() {
      alert(`我叫${name}，我${age}岁了，你好啊！`)
    }

    // 1.setup返回对象，对象中的属性、方法可以在模板中直接使用
    return {
      // name,
      age,
      sayHello
    }

    // 2.setup返回一个渲染函数，可以自定义渲染内容
    // 把h函数调用的返回值交出去
    // return () => h('h1', name)
  },
}
</script>