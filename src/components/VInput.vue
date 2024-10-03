<script setup>
import { ref } from 'vue'

const props=defineProps({
  modelValue: String,
  type: {
    type:String,
    default: 'text'
  }
})
const emit=defineEmits(['update:modelValue'])
const inputValue=ref(props.modelValue)
</script>

<template>
<div>
    <input :class="variant" :type="type" v-model="inputValue" type="text" @input="emit('update:modelValue',$event.target.value)"/>
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
