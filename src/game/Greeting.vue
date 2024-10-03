<script setup>

import TTButton from './TTButton.vue'

const emit = defineEmits(['startGame'])

function startGame() {
    emit('startGame')
}
</script>

<template>
    <div class="greeting">
        <div class="gameName">
            <span>Tic Tac Toe</span>
        </div>
        <TTButton
            label="Play"
            @click="startGame"  
        />
    </div>
</template>

<style scoped>
.greeting {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0 auto;
    padding-top: 40px;
    width: fit-content;
    height: fit-content;
    gap: 20px;
    font-family: 'Franklin Gothic Medium';
    font-size: 96px;
    color: #ffffff;
}

.gameName {
    display: flex;
    justify-content: center;
}
</style>