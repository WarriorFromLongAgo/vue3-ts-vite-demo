<script setup lang="ts">
import {ref, reactive, watchEffect, watch} from "vue";


const count = ref(0)
const handleCountAdd = () => {
  console.log("count = ", count)
  count.value++
  user.name = "李四"
  user.age++
}
const user = reactive({
  name: "张三",
  age: 12
})
const arr = reactive([1, 2, 3, 4, 5, 6, 7])
const originData = reactive({
  count2: 0, user2: {
    name: "张三2",
    age: 18
  },
  arr2: [1, 2, 3, 4]
})
const increment = () => {
  originData.count2++
  originData.user2.name = "李四"
}

watchEffect(() => console.log("watchEffect count = ", count.value))
watch(count, (newValue, oldValue) => console.log("watch = ", newValue, oldValue))

const props = defineProps({
  parentMsg: {
    type: String,
    default: () => "默认值"
  }
})

const emit = defineEmits(["on-change"])
const handleClick = () => {
  emit("on-change", '父组件的方法被调用了')
}

const childNode = () => {
  console.log("子组件的方法被调用了")
}
// 子组件暴露给信息给父组件，父组件通过ref，以及onMounted生命周期，获取到了子组件的数据
defineExpose({
  child: "我是暴露的子组件",
  childNode
})
</script>

<template>
  <p>{{ props.parentMsg }}</p>
  <button @click="handleClick">点击调用父组件的方法</button>
  <p>{{ count }}</p>
  <button @click="handleCountAdd">count增加</button>
  <p>{{ user.name }} {{ user.age }}</p>
  <p>{{ arr }}</p>
  <p v-for="(item, index) in originData" :key="index">
    {{ item }}
  </p>
  <button @click="increment">点击我变换第二个东西</button>
</template>