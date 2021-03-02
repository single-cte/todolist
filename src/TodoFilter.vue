<template>
  <!-- 过滤模块 -->
  <div class="filters">
     <!-- 给每个过滤选项注册点击事件,触发changefilter,并传递该过滤选项的value -->
    <span class="filter"
     v-for="filter in filters"
     :key = "filter.value"
     @click="$emit('change-filter', filter.value)"
     :class="{ active: selected === filter.value}">{{filter.label}}</span>
  </div>
</template>

<script>
export default {
  name: 'TodoFilter',
  props: ['selected'],
  setup () {
    const filters = [
      { label: '全部', value: 'all' },
      { label: '已完成', value: 'done' },
      { label: '未完成', value: 'todo' }
    ]
    return { filters }
  }
}
</script>

<style>
  /* 过滤 */
  .filters {
    margin: 20px 0;
    display: flex;
    justify-content: space-around;
    font-size: 20px;
    color: #808080;
  }

  .filter {
    cursor: pointer;
  }
  .filters .filter.active {
    color: #87CEEB;
  }

  #check-filter {
    font-size: 25px;
    color: orangered;
  }
</style>
