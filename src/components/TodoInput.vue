<template>
  <div>
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodoA">
    <button @click="addTodoA">추가</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoItem: ''
    }
  },
  methods: {
    addTodoA() {
      if (this.newTodoItem !== '') {
        let value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit('addTodoB', value);
        this.clearInput();
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  }
}
</script>