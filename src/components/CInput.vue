<script setup>
import { ref } from 'vue'

</script>

<template>
<div>
    <input :class="variant" v-model="inputValue" type="text" @input="emit('update:modelValue',$event.target.value)"/>
</div>
</template>

<style scoped>
input {
  padding: 6px 12px;
  border: 1px solid #614b37;
  background-color: #ececec;
  color: #614b37
}
input:hover {
    border: 1px solid #000000;
}
</style>
