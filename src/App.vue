<template>
  <section class="todoapp">
    <MyHeader @add="handleAdd" />
    <!-- 通过父组件==>子组件 -->
    <MyList :list="list" @del_item="handleClick" />
    <MyFooter :list="list" @childclick="zCf" />
  </section>
  <footer class="info">
    <p>双击待办项以编辑。</p>
  </footer>
</template>
<script setup>
import MyHeader from "@/components/MyHeader.vue";
import MyList from "@/components/MyList.vue";
import MyFooter from "@/components/MyFooter.vue";
// 引入ref响应声明对象
import { ref } from "vue";
const list = ref([
  { id: 100001, label: "Eat", status: false },
  { id: 100002, label: "Sleep", status: false },
  { id: 100003, label: "Playgames", status: false },
]);
//handleClick是一个删除方法
const handleClick = (id) => {
  console.log(id);
  //通过id 找索引  findIndex()用于查找数组中满足指定条件的第一个元素，并返回该元素的索引值
  const index = list.value.findIndex((item) => item.id == id);
  console.log(index);
  //splice(起始索引，删除元素的个数)
  list.value.splice(index, 1);
};
//从父组件接受到子组件传的值
const handleAdd = (x) => {
  //label传过来的值x
  const obj = { id: 100004, label: x, status: false };
  //push()方法用于向数组的末尾添加一个或多个元素，并返回修改后的数组的新长度
  list.value.push(obj);
  // console.log(list.value, 'app')
};
 const zCf = (value) => {
     list.value=value
 }
</script>
<style></style>
<!-- 软件技术4班乔志帅 221704412 -->
