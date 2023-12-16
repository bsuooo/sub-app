<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

function handleClick() {
  count.value++
  // 向主应用发送数据
  window.microApp.dispatch({count: count.value})
}

// 监听函数
function dataListener (data) {
  const { count: c } = data
  count.value = c
}

// 监听数据变化
// window.eventCenterForChildApp_1.addDataListener(dataListener, true)
// console.log(window.eventCenterForChildApp_1, 2);

// 监听数据变化，初始化时如果有数据则主动触发一次
window.microApp.addDataListener(dataListener, true)

// 解绑监听函数
// window.microApp.removeDataListener(dataListener)

// 清空当前子应用的所有绑定函数(全局数据函数除外)
// window.microApp.clearDataListener()

const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="handleClick">count is {{ count }}</button>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
