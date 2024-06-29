<template>
  <header class="header">
    <h1>todos</h1>
    <!-- @绑定键盘事件 按下回车enter触发事件 -->
    <input autofocus="autofocus" autocomplete="off" placeholder="您的待办事项是?" class="new-todo" @keyup.enter="handleAdd"
      v-model="text">

  </header>
</template>
<script setup>
import { ref } from 'vue';
//声明响应式text 
const text = ref('');
//defineEmits子向父传值
const emit = defineEmits(['add'])
//在输入框添加text输入内容的方法
const handleAdd = () => {
  emit('add', text.value)
  text.value=''
}
</script>
<style></style>