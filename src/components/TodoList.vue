<template>
  <section>
    <ul>
      <li v-for="({id, text, isDone}, idx) in propsData" :key="idx">
        <input type="checkbox">
        <label @dblclick="updateTodoA">{{ text }}</label>
        <input type="text" class="edit">
        <button class="btn-del" @click="removeTodoA(idx, id, text)">삭제</button>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: {
    propsData: {type: Array, default: () => []}
  },
  methods: {
    removeTodoA(idx, id, text) {
      this.$emit('removeTodoB', idx, id, text);
    },
    updateTodoA() {
      this.$emit('updateTodoB');
    }
  }
}
</script>

<style scoped>
input[type=checkbox] {display: none;}
ul {
  padding: 0;
  margin: 0;
  list-style: none;
}
.edit {display: none;}
.editing .edit {display: inline-block;}
.editing label {display: none;}
</style>