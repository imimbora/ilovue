<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput @addTodoB="addTodoC"></TodoInput>
    <TodoList :propsData="todoArray" @removeTodoB="removeTodoC" @updateTodoB="updateTodoC"></TodoList>
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
      todoArray: []
    }
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        let keyDate = localStorage.key(i);
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          let dataString = localStorage.getItem(keyDate);
          let dataJson = JSON.parse(dataString);
          this.todoArray = [
            ...this.todoArray,
            dataJson
          ]
        }
      }
    }
    console.log(this.todoArray);
  },
  methods: {
    addTodoC(text) {
      let newItem = {
        id: Date.now(),
        text,
        isDone: false
      };
      localStorage.setItem(newItem.id, JSON.stringify(newItem));
      this.todoArray.push(newItem);
    },
    removeTodoC(idx, id, text) {
      // console.log(idx, id, text)
      localStorage.removeItem(id);
      this.todoArray.splice(idx, 1);
    },
    clearAllC() {
      localStorage.clear();
      this.todoArray = [];
    },
    updateTodoC() {
      console.log('받긴 했는데');
    }
  }
}
</script>

<style>
body {text-align:center; background-color:#f6f6f8;}
</style>