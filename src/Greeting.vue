<script setup>
defineProps({
  label: String,
})
</script>

<template>
    <div>
        <div><span></span></div>
    </div>
</template>

<style scoped>
button {
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