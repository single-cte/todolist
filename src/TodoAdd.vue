<template>
 <!-- 添加模块 -->
 <div class="input">
  <input type="text" name="add"
   autocomplete="off" required oninvalid="setCustomValidity('请输入QQ号码！');"
   v-model="todoContent"
   @keyup.enter="emitAddTodo">
  <button @click="emitAddTodo">
   <i class="add-button">添加</i>
  </button>
 </div>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'TodoAdd',
  props: ['tid'],
  setup (props, context) {
    const todoContent = ref('')
    const emitAddTodo = () => {
      const todo = {
        id: props.tid,
        content: todoContent.value, // 将input的内容作为todo的值
        flag: false
      }
      context.emit('add-todo', todo)// 触发addtodo事件，把todo作为参数传递给事件
      todoContent.value = ''// 清空输入框
    }
    return {
      todoContent,
      emitAddTodo
    }
  }
}
</script>

<style>
 /* 添加 */
 .input {
  position: relative;
  display: flex;
  align-items: center;
 }

 .input input {
  padding: 16px 60px 16px 16px;
  outline: none;
  border: none;
  border-radius: 25px;
  box-shadow: rgba(0, 0, 0, 0.05);
  width: 100%;
  font-size: 16px;
  color: grey;
 }

 .input button {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: linear-gradient(rgb(145,184,239), rgb(177,221,246));
  border: none;
  outline: none;
  color: white;
  position: absolute;
  right: 0;
  cursor: pointer;
 }
</style>
