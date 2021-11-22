# 父传子

父组件向子组件传递一个数据，可以用这两种方式：

v-bind
refs获取子组件内部某个函数，直接调用传参（这里简称refs方式）
refs方式
关于v-bind咱们就不细说了，在基本操作章节已经讲过其对应的使用方式了。这小节主要在中讲Vue3如何通过ref获取子组件实例并调用其身上的函数来对子组件进行传值。

## 子组件

```ts 
<template>
  // 渲染从父级接受到的值
  <div>Son: {{ valueRef }}</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
export default defineComponent({
  name: 'Son',
  setup() {
    const valueRef = ref('')
    

    // 该函数可以接受父级传递一个参数，并修改valueRef的值
    const acceptValue = (value: string) => (valueRef.value = value)
    
    return {
      acceptValue,
      valueRef
    }
  }
})
</script>
```

## 父组件



```ts
<template>
  <div>sonRef</div>
  <button @click="sendValue">send</button>
  // 这里ref接受的字符串，要setup返回的ref类型的变量同名
  <Son ref="sonRef" />
</template>


<script lang="ts">
import { defineComponent, ref } from 'vue'
import Son from '@/components/Son.vue'

export default defineComponent({
  name: 'Demo',
  components: {
    Son
  },
  setup() {
    // 如果ref初始值是一个空，可以用于接受一个实例
    // vue3中获取实例的方式和vue2略有不同
    const sonRef = ref()
const sendValue = () => {
  // 可以拿到son组件实例，并调用其setup返回的所有信息
  console.log(sonRef.value)
  
  // 通过调用son组件实例的方法，向其传递数据
  sonRef.value.acceptValue('123456')
}

return {
  sonRef,
  sendValue
}
  }
})
</script>
```


这里可以看一下流程图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201216205448160.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzI3OTYy,size_16,color_FFFFFF,t_70)

Vue2中使用this.$refs，this.$children的方式很相似，都是通过拿到子组件实例，直接调用子组件身上的函数。方法千篇一律，不过在Vue3中没有了this这个黑盒。

这里我们可以在控制台看一下这个sonRef.value是一个怎样的东西。

可以发现，通过ref获取到的子组件实例上面可以拿到setup返回的所有变量和方法，同时还可以拿到其他的一些内部属性。我们可以看一下官方文档Vue 组合式 API的描述。

在 Virtual DOM patch 算法中，如果一个 VNode 的 ref 对应一个渲染上下文中的 ref，则该 VNode对应的元素或组件实例将被分配给该 ref。这是在 Virtual DOM 的 mount / patch 过程中执行的，因此模板 ref仅在渲染初始化后才能访问。

ref方式总结

优点：

父组件可以获取快速向确定存在的子组件传递数据
传递的参数不受限制，传递方式比较灵活
缺点：

ref获取的子组件必须确定存在的（不确定存在的情况：如插槽上子组件，v-if控制的子组件）
子组件还需要实现接受参数的方法