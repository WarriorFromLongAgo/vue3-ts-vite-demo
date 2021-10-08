<script setup lang="ts">
import TestPropsEmit from "./components/test-props-emit/index.vue"
import {ref, onMounted} from "vue"

// 父组件的方法
const handleChange = (params: string) => {
  console.log("handlerChange = ", params)
}
const parentMsg = ref("这是父组件传递给子组件的数据")

// 子组件暴露给信息给父组件，父组件通过ref，以及onMounted生命周期，获取到了子组件的数据
const propsEmitRef = ref()
onMounted(() => {
  console.log("propsEmitRef = ", propsEmitRef)
  console.log("propsEmitRef = ", propsEmitRef.value.child)
  console.log("propsEmitRef = ", propsEmitRef.value.childNode())
})

</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png"/>
  <!--  onchange 是子组件的方法-->
  <!--  parentMsg 是父组件的信息-->
  <TestPropsEmit ref="propsEmitRef" :parentMsg="parentMsg" @on-change="handleChange"></TestPropsEmit>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
