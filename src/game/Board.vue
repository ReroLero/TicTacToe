<script setup>
import BoardRow from './BoardRow.vue';

const props = defineProps({
    board: {
        type: Array,
        required: true
    },
    gameEnded: {
        type: Boolean,
        default: false
    },
    winningCells: {
        type: Array,
    },
})

const emit = defineEmits(['click'])

// METHODS
function onCellClick(rowIndex, cellIndex) {
    emit('click', { rowIndex, cellIndex })
}

function getRowWinningCells(rowIndex) {
    if (props.winningCells === undefined) 
        return []

    return props.winningCells
        .filter((cell) => +cell.split(':')[0] === rowIndex)
        .map((cell) => cell.split(':')[1])
}
</script>

<template>
    <div class="board">
        <BoardRow 
            v-for="(row, index) in board" :key="index"
            :row="row" 
            :row-index="index"
            :game-ended="gameEnded"
            :winning-cells="getRowWinningCells(index)"
            @click="onCellClick(index, $event)"
        />
    </div>
</template>

<style scoped> 

.board {
    z-index: 1;
    padding: 20px;
    background-color: #3F3F3F;
    border-radius: 20px;
    box-shadow:  inset 6px 6px 8px 0px #9F9F9F, inset 0px -0.025px 4px 0px #525252, inset -12px -12px 8px 0px #2b2b2b;
}
</style> 