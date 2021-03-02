<template>
 <!-- 列表模块 -->
 <div class="todo-list">
  <todo-list-item
   :key="todo.id"
   v-for="todo in todos"
   :todo-item = "todo"
   @del-todo="delTodo"
   @change-state = "todo.flag = $event.target.checked"
   >
   </todo-list-item>
 </div>
</template>

<script>
import TodoListItem from './TodoListItem.vue'
export default {
  name: 'TodoList',
  components: {
    TodoListItem
  },
  props: ['todos'],
  setup (props, context) {
    const delTodo = (i) => {
      context.emit('del-todo-list', i)
    }
    return {
      // emitDelTodo
      delTodo
    }
  }
}
</script>

<style>
</style>
