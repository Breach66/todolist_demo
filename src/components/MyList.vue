<script setup>
defineProps({
  list: {
    type: Array,
    //default默认为 空数组
  }
})
</script>
<template>
  <section class="main">
    <input type="checkbox" class="toggle-all" />
    <ul class="todo-list">
       <!-- v-for='' 循环父组件传过来的list列表  -->
      <li class="todo" :class="{ completed: item.status }" v-for="item in list" >
        <div class="view">
          <!-- item.label对象里面的value值 v-model=''双向绑定事件           -->
          <input type="checkbox" v-model='item.status' class="toggle" /> <label>{{ item.label
            }}</label>
          <!-- 绑定单击事件 @click=''               $emit(事件名称参数,)自定义事件-->
          <button class="destroy" @click="$emit('del_item', item.id)"></button>
        </div>
      </li>

    </ul>
  </section>


</template>

<style></style>