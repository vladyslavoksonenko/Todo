<template>
  <div id="app">
    <div>
      <h2 class="title">Список дел</h2>
      <h5 class="time">{{date.nowDate}}</h5>
      <AddTodo v-on:addNewTodo="addTodo" />
      <FilterTodo v-on:sort-todo="sortTodoList" />
      <TodoList
          v-bind:todoList=sortTodo
          v-on:deletedItem="deletedItem"
      />
    </div>
  </div>
</template>

<script>

import TodoList from "./components/TodoList.vue";
import AddTodo from "./components/AddTodo.vue";
import FilterTodo from "./components/FilterTodo";


export default {
  name: 'App',
  components: {
    FilterTodo,
    AddTodo,
    TodoList
  },
  data () {
    return {
      todoList: [],
      date: {
        nowDate: new Date()
      },
      statusSort: "all"
    }
  },
  created() {
    let data = localStorage.getItem("todoList")
    if (data === null) {
      localStorage.setItem("todoList", "[]")
    }
    data = localStorage.getItem("todoList")
    this.todoList = JSON.parse(data);

    setInterval(() => {
      this.date.nowDate = new Date()
    }, 1000)
  },
  computed: {
    sortTodo() {
      const todo = this.todoList
      if (this.statusSort === 'all') {
        return todo.sort((item, prevItem) => item.id - prevItem.id)
      }
      if (this.statusSort === "work") {
        console.log("Sort work")
        return todo.sort((item, prevItem) => {
          if (item.completed === prevItem.completed) {
            return 0;
          } else {
            if (!item.completed) {
              return -1
            } else {
              return 1
            }
          }
        })
      }
      if (this.statusSort === "finished") {
        console.log("Sort finished")
        return todo.sort((item, prevItem) => {
          if (item.completed === prevItem.completed) {
            return 0;
          } else {
            if (item.completed) {
              return -1
            } else {
              return 1
            }
          }
        })
      }
      return todo
    }
  },
  watch: {
    todoList: {
      handler() {
        const stringData = JSON.stringify(this.todoList)
        localStorage.setItem("todoList", stringData)
      },
      deep: true
    }

  },
  methods: {
    addTodo(newTodo) {
      this.todoList.push(newTodo)
    },
    deletedItem(idItem) {
      this.todoList = this.todoList.filter((todo) => todo.id !== idItem)
    },
    sortTodoList(sortValue) {
      this.statusSort = sortValue;

    },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap');
body {
  font-family: 'Lato', sans-serif;
  background: #06276F;
  color: #fff;
}
#app {
  max-width: 400px;
  margin: auto;
}
.title {
  text-align: center;
}
.time {text-align: center}
</style>
