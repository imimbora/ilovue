<template>
  <div>
    <button type="button" @click="clearAllA">모두 삭제</button>
  </div>
</template>

<script>
  export default {
    methods: {
      clearAllA() {
        this.$emit('clearAllB')
      }
    }
  }
</script>