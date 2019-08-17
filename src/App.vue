<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput @addTodoB="addTodoC"></TodoInput>
    <TodoList :propsData="todoItems" @removeTodoB="removeTodoC" @updateTodoA="updateTodoB"></TodoList>
    <TodoFooter @clearAllB="clearAllC"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  },
  data() {
    return {
      todoItems: [
        {
          id: 12345678,
          text: "밥먹기",
          isDone: true
        },
        {
          id: 12345679,
          text: "Vue 뿌시기",
          isDone: false
        },
        {
          id: 12345680,
          text: "청소하기",
          isDone: false
        }
      ]
    }
  },
  methods: {
    addTodoC(text) {
      let newItem = {
        id: Date.now(),
        text,
        isDone: false
      };
      this.todoItems.push(newItem);
    },
    removeTodoC(idx, id, text) {
      this.todoItems.splice(idx, 1);
    },
    clearAllC() {
      this.todoItems = [];
    },
    updateTodoB({ id, text }) {
      const todoItems = [...this.todoItems];
      const todo = todoItems.find(todo => todo.id === id);
      if (todo) {
        todo.text = text;
        this.todoItems = todoItems;
      }
    }
  }
}
</script>

<style>
body {text-align:center; background-color:#f6f6f8;}
</style>