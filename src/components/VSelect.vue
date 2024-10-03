<script setup>
import { ref } from 'vue'
const props=defineProps({
modelValue:String,
options:Array
  }
)
const emit=defineEmits(['update:modelValue'])
const selectValue=ref(props.modelValue)
function setSelectedValue(event){
const selectedValue=event.target.value
emit('update:modelValue',selectedValue)
}
</script>

<template>
  <select name="select" required="false" @change="setSelectedValue">
    <option v-for="option in options" :value="option">{{ option }}</option>
  </select>
</template>

<style scoped>
select{
  padding: 6px 12px;
  border: 1px solid #614b37;
  background-color: #ececec;
  color: #614b37
}
</style>
