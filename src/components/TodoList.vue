<template>
  <section>
    <ul>
      <li
        :class="{editing: edit.id === id}"
        v-for="({id, text, isDone}, idx) in propsData" :key="idx">
        <input type="checkbox">
        <label @click="handleEdit({ id, text })">{{ text }}</label>
        <input type="text" class="edit" v-model="edit.text" @keypress="handleUpdate">
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
  data() {
    return {
      edit: {
        text: "",
        id: -1
      }
    }
  },
  methods: {
    removeTodoA(idx, id, text) {
      this.$emit('removeTodoB', idx, id, text);
    },
    handleEdit({ id, text }) {
      this.edit = {
        id,
        text
      };
    },
    handleUpdate({ keyCode }) {
      if (keyCode === 13) {
        this.$emit("updateTodoA", this.edit);
        this.edit = {
          id: -1,
          text: ""
        }
      }
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
ul li {padding:10px 0;}
.edit {display: none;}
.editing .edit {display: inline-block;}
.editing label {display: none;}
</style>