<template>
 <div class="todo-item" :class="{done: todoItem.flag}">
  <label>
    <span class="check-button" :class="{check: todoItem.flag}"></span>
   <input type="checkbox" :checked="todoItem.flag" @click="$emit('change-state', $event)">
   <div class="content">{{todoItem.content}}</div>
  </label>
    <span class="del" @click="emitDelTodo">删除</span>
 </div>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: ['todoItem'],
  setup (props, context) {
    const emitDelTodo = () => {
      context.emit('del-todo', props.todoItem.id)
    }
    return {
      emitDelTodo
    }
  }
}
</script>

<style>
 /* 列表 */
 .todo-item {
  position: relative;
  background-color: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 8px;
  color: grey;
 }
 .todo-item .content {
   display: inline-block;
   width: 340px;
   user-select:none;
 }
 .todo-item label {
  width: 350px;
 }
 .todo-item.done .content{
   text-decoration: line-through;
   font-style: italic;
 }

 .todo-item span.check-button {
  top: 0px;
 }

 /* 添加伪元素 */
 .todo-item span.check-button {
  content: '';
  display: block;
  position: absolute;
  left: 10px;
  top: 50%;
  width: 18px;
  height: 18px;
  background-color: white;
  border-radius: 50%;
  transform: translate(0, -50%);
  border: 1px solid #b382f9;
 }

 .todo-item span.check-button.check {
  background: linear-gradient(rgb(145,184,239), rgb(177,221,246));
 }
 /* 删除功能 */
.del {
  position: absolute;
  top: 50%;
  transform: translate(0, -50%);
  right: 20px;
  color: darkorange;
  cursor: pointer;
  user-select:none;
}

 /* 隐藏原来的复选框 */
 .todo-item input {
  opacity: 0;
  margin-right: 16px;
 }

 /* 将选中元素的after伪元素显示 */
 .todo-item input:checked + .check-button::after {
  opacity: 1;
 }
</style>
