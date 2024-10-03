<script setup>
import Board from '../game/Board.vue';
import History from '../game/History.vue';
</script>

<template>
    <div class="panel">
        <Board></Board>;
        <History></History>
    </div>;
</template>

<style scoped> 
.panel {
    width: fit-content;
    height: fit-content;
    flex-direction: row;
    gap: 44px;
}
</style> 