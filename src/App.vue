<script setup>
import { onMounted } from 'vue'
// 1. 导入use打头的方法  useCounterStore
import { useCounterStore } from '@/stores/counters'
import { storeToRefs } from 'pinia';

// 2. 执行方法得到store实例对象
const counterStore = useCounterStore()
console.log(counterStore);

// 直接解构赋值（响应式丢失）
//const { count, doubleCount } = counterStore

// 方法包裹，保持响应式更新
const { count, doubleCount } = storeToRefs(counterStore)

//方法直接从原来的counterStore中解构赋值
const { increment } = counterStore


onMounted(() => {
  counterStore.getList()
})
</script>

<template>
  <button @click="increment()">{{ count }}</button>
  <div>{{ doubleCount }}</div>
  <ul>
    <li v-for="item in counterStore.list" :key="item.id">{{ item.name }}</li>
  </ul>
</template>

<style scoped>
</style>
