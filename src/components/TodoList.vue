<template>

    <div>
      <template v-if="todoList.length">
        <hr>
        <div class="todo-list" v-for="(item, i) in todoList" v-bind:key="item.id">
          <TodoItem
              v-bind:item="item"
              v-bind:index="i"
              v-on:deletedItem="deletedItem"
              v-on:completed-item="completedItem"
          />
        </div>
        <hr>
      </template>
      <template v-else>
        <h3>Записей пока нет.</h3>
      </template>
    </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "TodoList",
  components: { TodoItem },
  props: ["todoList"],
  methods: {
    deletedItem(idItem) {
      this.$emit("deletedItem", idItem )
    },
    completedItem(idItem, isCompleted) {
      this.$emit("completed-item",idItem, isCompleted)
    }
  }
}
</script>

<style scoped>
.todo-list {
  background: #6C8DD5;
  margin-bottom: 10px;
  border-radius: 5px;
}
hr {
  border: 1px solid #6C8DD5;
}
</style>