<template>
  <form @submit.prevent="handleSubmit"><input type="text" v-model="text"></form>
</template>

<script setup>

  import { ref, defineEmits } from 'vue'

  const text = ref("");
  const emits = defineEmits(["onNewItem"])
  
  function handleSubmit() {
    if (text !== "") {
      // Manda a llamar al emit
      emits("onNewItem", text);
      text.value = ""; 
    }
  }
</script>

<style scoped>
form {
  margin-bottom: 10px;
}
input {
  width: 100px;
  box-sizing: border-box;
}
</style>