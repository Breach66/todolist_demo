<script setup>
import { ref, reactive, computed, watch,defineEmits } from 'vue';
// 父组件---->
// <MyFooter :list="list" @childclick="zCf" />
// const zCf = (value) => {
//     list.value=value
// }
const datalist = ref(0);
const falseList = ref(0);
const errData = ref(0);

// 已完成数据
const errordata= ref([]);


const emit = defineEmits(['childclick'])

const props = defineProps({
  list: {
    type: Array,
    required: true
  }
});
//同过父组件传过来的list中的数组打印的内容
// console.log(props.list);
//监听父组件变化后传过来的值
watch(
  props.list,
  //两个参数一个新变化的值and一个没有变化的值
  (obj, list) => {
    console.log(obj);
  }
);
const publishedBooksMessage = computed(() => {
  datalist.value = 0;
  props.list.forEach(item => {
    //当数据状态为已完成的时候计数器加一
    if (item.status) {
      datalist.value++;
    }
  });
  return datalist.value;
});
const handlefalseList = computed(() => {
  falseList.value = 0;
  errordata.value=[]
  props.list.forEach(item => {
    //当数据状态为未完成的时候计数器加一
    if (!item.status) {
      errordata.value.push(item)
      falseList.value++;
    }
  });
  errData.value = falseList.value; //
  return falseList.value;
});
const handleClickTue = () => {
    emit('childclick',errordata.value)
}
</script>
<template>
  <footer class="footer">
    <span class="todo-count"> {{ `有${errData}个未完成` }} </span>
    <span class="todo-count"> </span>
    <ul class="filters">
      <li>
        <a href="#/all" class="selected"> 全部：{{ list.length }}</a>
      </li>
      <li>
        <a href="#/active" class="">未完成{{ handlefalseList }}</a>
      </li>
      <li>
        <a href="#/completed" class="">已完成{{ publishedBooksMessage }}</a>
      </li>
    </ul>
    <!-- 绑定单击事件删除内容 -->
    <button class="clear-completed" @click="handleClickTue">清除已完成</button>
  </footer>
</template>

<style></style>
