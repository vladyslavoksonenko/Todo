<template>
  <div class="add-block">
    <div class="inputs">
      <div class="add-input-block">
        <input
            v-model="newTodo.title"
            v-on:keydown.enter="createPost"
            class="add-input" type="text">
          <template v-if="!inputValidation">
            <span class="valid-add">Введите текст</span>
          </template>
      </div>
      <button
          v-on:click="createPost"
          class="add-button"
          value="">Add</button>
    </div>
    <div class="valid-block">
    </div>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data () {
    return {
      newTodo: {
       id: null,
        title: "",
        completed: false,
        createTime: null,
        completedTime: null
      },
      inputValidation: true

    }
  },
  watch: {
    'newTodo.title': function () {
      if (this.title !== "") {
        this.inputValidation = true
      }
    }
  },
  methods: {
    createPost() {
      if (this.newTodo.title !== "") {
        this.newTodo.createTime = new Date()
        this.newTodo.id = Date.now();
        this.$emit('addNewTodo', this.newTodo);
        this.newTodo = {
          id: null, title: "", completed: false
        }
      } else {
        this.inputValidation = false;
      }

    }
  }
}
</script>

<style scoped>
  .inputs {
    display: flex;
  }
  .add-input-block {
    position: relative;
  }
  .add-block {
    text-align: center;
    margin-bottom: 20px;
    display: flex;
    justify-content: center;
  }
  .add-input {
    width: 200px;
    padding: 10px;
    font-size: 17px;
    border: 3px solid #2A4580;
    border-radius: 5px;
    color: #000;
    background: #6C8DD5;
    color: #fff;
    margin-right: 10px;
  }
  .add-button {
    padding: 10px 15px;
    font-size: 17px;
    border: 3px solid #FFA900;
    border-radius: 5px;
    color: #fff;
    background: #FFA900;
    cursor: pointer;
  }

  .add-button:hover {
    background: #BF8F30;
    border: 3px solid #BF8F30;
  }
  .valid-add {
    position: absolute;
    color: #6C8DD5;
    font-size: 14px;
    left: 0;
    top: -20px;
  }
</style>