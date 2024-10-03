<script setup>
import { ref } from 'vue'
import TTButton from '../game/TTButton.vue';

const props=defineProps()
const emit = defineEmits(['resetGame'])

function onResetGame() {
    emit('resetGame')
}
</script>

<template>
    <div class="toast">
        <img src="../assets/Toast.svg" >
        <span>Congrats you won !</span>
        <button class="link" @click="onResetGame"><span>restart</span> </button>
    </div>
</template>

<style scoped>
.toast{
    width: fit-content;
    display: flex;
    justify-content: center;
    gap: 12px;
    position: fixed;
    left: 50%;
    top: 5%;
    transform: translateX(-50%);
    color: #dbdbdb;
    background-color: #444444;
    padding: 8px 16px;
    border-radius: 8px;
    font-size: 32px;
    text-transform: uppercase;
    box-shadow: 8px 8px 8px 4px #242424;
}

.link {
    color: #242424;
    border: transparent;
    padding: 0px 4px;
    background-color: transparent;
    font-size: 32px;
    text-transform: uppercase;
}
.link:hover {
    color: #ffffff;
}
</style>