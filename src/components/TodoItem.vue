<template>

  <div
      v-on:click.stop="completedTodo"
      v-bind:class="{completed: item.completed}"
      v-bind:title="item.completedTime"
      class="item"
  >
    <hr class="hr" v-bind:class="{completed: item.completed}">
    <input type="checkbox" class="checkbox" v-model="item.completed">
    <div class="time">
    </div>
    <span class="title">{{item.title}}</span>
    <button v-bind:class="{completed: item.completed}" v-on:click.stop="deleted">Deleted</button>
  </div>

</template>

<script>
export default {
  name: "TodoItem",
  props: {
    item: {
      type: Object
    },
    index: {
      type: Number
    }
  },
  methods: {
    deleted() {
      this.$emit("deletedItem", this.item.id)
    },
    completedTodo() {
      if (this.item.completed) {
        this.item.completed = false
        this.item.completedTime = null

      } else {
        this.item.completed = true
        this.item.completedTime = new Date()
      }
      this.$emit("completed-item", this.item.id, this.item.completed)
    }
  },
}
</script>

<style scoped>
  .item {
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 18px;
    border: 2px solid #2A4580;
    border-radius: 5px;
    position: relative;
    font-size: 17px;
  }
  span.title {
    width: 100%;
    margin: auto;
  }

  .checkbox {
    transform:scale(1.3);
    opacity:0.9;
    cursor:pointer;
  }

  .item.completed {
    background: #4573D5;
    color: #2A4580;
  }
  .hr {
    display: none;
  }
  .hr.completed {
    display: block;
    position: absolute;
    width: 43%;
    border: 1px solid #06276F;
    margin: auto;
  }
  button {
    background: #2A4580;
    border-radius: 5px;
    color: #fff;
    padding: 5px;
    border: 1px solid #fff;
    cursor: pointer;
  }
  button.completed {
    background: #4573D5;
  }

  button.completed:hover {
    background: #2A4580;
  }

  button:hover {
    background: #4573D5;
  }


</style>