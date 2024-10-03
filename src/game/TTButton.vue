<script setup>

defineProps({
  label: String,
})
</script>

<template>
 <button>
    {{ label }}
  </button>
</template>


<style scoped> 
button {
    text-transform: uppercase;
    width: 100%;
    height: 48px;
    padding: 6px 12px;
    font-size: 18px;
    letter-spacing: 2px;
    color: #ffffff;
    background-color: #303030;
    border: none;
    border-radius: 8px;
    box-shadow: 2px 2px 12px #000000, -4px -4px 16px #242424, inset 4px 4px 8px #303030, inset -2px -2px 2px #303030;
}

button:hover{
    cursor: pointer;
    background-color: #414141;
    color: #ffffff;
    transition-duration: 350ms;
    transition-property: all;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: 2px 2px 12px #303030, -4px -4px 16px #242424, inset 4px 4px 4px #303030, inset -2px -2px 2px #303030;
}
button:active{
    cursor: pointer;
    font-size: 14px;
    background-color: #303030;
    color: #cfcfcf;
    transition-duration: 150ms;
    transition-property: all;
    transition-timing-function: cubic-bezier(0.1, 0, 0.1, 1);
    box-shadow: 2px 2px 12px #303030, -2px -2px 16px #303030, inset 8px 8px 12px #303030, inset -2px -2px 8px #303030;
}
</style>