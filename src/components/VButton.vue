<script setup>
defineProps({
  label: String,
  variant:{
    type:String,
    default:'primary'
  }
})
</script>

<template>
 <button :class="variant">
    {{ label }}
  </button>
</template>

<style scoped>
button {
  font-size: 24px;
  padding: 6px 12px;
  transition-duration: 400ms;
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}
button.primary {
  border: 1px solid #614b37;
  background-color: #614b37;
  color: #ececec;
}
button.primary:hover {
  background-color: #4d3926;
  border: 1px solid #4d3926;
  cursor: pointer;
}
button.secondary {
  border: 1px solid #614b37;
  background-color: #ececec;
  color: #614b37
}
button.secondary:hover {
  background-color: #4d3926;
  border: 1px solid #4d3926;
  color: #ececec;
  cursor: pointer;
}
</style>
