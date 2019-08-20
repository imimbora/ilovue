<template>
  <section>
    <ul>
      <li
        :class="{editing: edit.id === id}"
        v-for="({id, todo}) in propsData" :key="id">
        <input type="checkbox">
        <label @click="handleEdit({ id, todo })">{{ todo }}</label>
        <input type="text" class="edit" v-model="edit.todo" @keypress="handleUpdate">
        <button class="btn-del" @click="removeTodoA(id)">삭제</button>
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
        todo: "",
        id: -1
      }
    }
  },
  methods: {
    removeTodoA(id) {
      this.$emit('removeTodoB', id);
    },
    handleEdit({ id, todo }) {
      this.edit = {
        id,
        todo
      };
    },
    handleUpdate({ keyCode }) {
      if (keyCode === 13) {
        this.$emit("updateTodoA", this.edit);
        this.edit = {
          id: -1,
          todo: ""
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