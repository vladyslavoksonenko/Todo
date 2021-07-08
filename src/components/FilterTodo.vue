<template>
  <div class="sort-btns">
    <span class="sort-title">Сортировка:</span>
    <button v-bind:class="(active === 'all') ? 'active' : ''" v-on:click="sortTodo('all')">По умолчанию</button>
    <button v-bind:class="(active === 'work') ? 'active' : ''" v-on:click="sortTodo('work')">В работе</button>
    <button v-bind:class="(active === 'finished') ? 'active' : ''" v-on:click="sortTodo('finished')">Завершенные</button>
  </div>
</template>

<script>
export default {
  name: "FilterTodo",
  data() {
    return {
      active: null
    }
  },
  props: {
    type: Object
  },
  methods: {
    sortTodo(isCompleted) {
      this.$emit("sort-todo", isCompleted);
      this.active = isCompleted;

    }
  }
}
</script>

<style scoped>
  .sort-title {
    font-size: 12px;
  }
  .sort-btns {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  button {
    background: #2A4580;
    border-radius: 5px;
    color: #fff;
    padding: 5px;
    border: 1px solid #fff;
    cursor: pointer;
    margin-right: 5px;
  }
  button.active {
    background: #4573D5;
  }
  button:hover {
    background: #4573D5;
  }
</style>