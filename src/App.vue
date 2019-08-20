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
import axios from 'axios'

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
      todoItems: []
    }
  },
  methods: {
    addTodoC(text) {
      /* let newItem = {
        id: Date.now(),
        text,
        isDone: false
      }; */
      // this.todoItems.push(newItem);

      let url = 'http://127.0.0.1:5000/todo/'

      axios.post(url, {
        todo: text
      }).then(res => {
        console.log(res)
      })
      this.getTodo()
    },
    removeTodoC(id) {
      // this.todoItems.splice(idx, 1);
      let url = `http://127.0.0.1:5000/todo/${id}`

      axios.delete(url).then(res => {
        console.log(res)
      })
      
      this.getTodo()
    },
    clearAllC() {
      this.todoItems = [];
    },
    updateTodoB({ id, todo }) {
      // console.log(id)
      // console.log(todo)

      let url = `http://127.0.0.1:5000/todo/${id}`
      axios.put(url, {
        todo: todo
      }).then(res => {
        // console.log(res)
        const todoItems = [...this.todoItems];
        const todo_ = todoItems.find(todo_ => todo_.id === id);
        if (todo_) {
          todo_.todo = todo;
          this.todoItems = todoItems;
        }
      })
    },
    getTodo(){
      let url = 'http://127.0.0.1:5000/todo/'
      axios.get(url).then(res => {
        this.todoItems = res.data.data
        console.log(res.data.data)
      })
    }
  },
  mounted(){
    // console.log('mounted')
  },
  created(){
    // console.log('created')
    this.getTodo()
  }
}
</script>

<style>
body {text-align:center; background-color:#f6f6f8;}
</style>