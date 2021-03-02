<template>
  <main>
    <div class="container">
      <!-- 头部模块 -->
      <div class="todo">
        <h1>欢迎使用todolist</h1>
        <todo-add :tid="todos.length" @add-todo="addTodo" />
        <todo-filter :selected="filter" @change-filter="filter = $event" />
        <todo-list :todos="filteredTodos" @del-todo-list="delTodoList"/>
      </div>
    </div>
  </main>
</template>

<script>
import { ref, computed } from 'vue'
import TodoAdd from './TodoAdd.vue'
import TodoFilter from './TodoFilter.vue'
import TodoList from './TodoList.vue'
export default {
  name: 'App',
  components: {
    TodoAdd,
    TodoFilter,
    TodoList
  },
  setup () {
    const todos = ref([])
    // ref包装的属性需要value才能访问到数据，template中vue自动拆解出value
    const addTodo = (data) => {
      const trimData = data.content.trim()
      if (trimData !== '') {
        todos.value.push(data)
      }
    } // 事件接收参数todo并添加到todos里
    const delTodoList = (i) => {
      const x = todos.value.findIndex(x => x.id === i)
      todos.value.splice(x, 1)
    }
    const filter = ref('all')
    // 通过计算属性得到一个符合条件的数组
    const filteredTodos = computed(() => {
      switch (filter.value) {
        case 'done':
          return todos.value.filter((todo) => todo.flag)
        case 'todo':
          return todos.value.filter((todo) => !todo.flag)
        default:
          return todos.value
      }
    })
    return {
      // 为了在template中使用数据和函数
      todos,
      addTodo,
      delTodoList,
      filter,
      filteredTodos
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: helvetica, "microsoft yahei";
  }

  ul li {
    list-style: none;
  }

  /* 背景 */
  main {
    width: 100vw;
    min-height: 100vh;
    /* background-color: skyblue; */
    background: linear-gradient(rgb(145,184,239), rgb(177,221,246));
    display: flex;
    align-items: center;
    justify-content: center;
  }

  /* 主体 */
  .container {
    width: 500px;
    box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15);
    border-radius: 24px;
    padding: 0 30px 50px;
    background-color: rgb(245, 246, 252);
  }

  /* 头部 */
  h1 {
    margin: 25px 0;
    font-size: 28px;
    color: dimgray;
    text-align: center;
  }
</style>
