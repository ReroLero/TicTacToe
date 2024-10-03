<script setup>
import BoardCell from './BoardCell.vue';
import {computed} from 'vue'

const props = defineProps({
    // [string, string, string]
    row: {
        type: Array,
        required: true
    },
    rowIndex: Number,
    gameEnded: {
        type: Boolean,
        default: false
    },
    winningCells: {
        Type: Array,
        default: ()=>([]),
    },

})

const emit = defineEmits(['click'])

// COMPUTED
const placement = computed(() => {
    if(props.rowIndex === 0)
        return 'top'
    else if(props.rowIndex === 1)
        return 'center'
    else
        return 'bottom'
})

// METHODS
function isWinningCell(cellIndex) {
    return !!props.winningCells.find((cell) => +cell === cellIndex)
} 
</script>

<template>
    <div class="board-row">
        <BoardCell 
            v-for="(cell, index) in row" :key="index"
            :variant="cell"
            :placement="placement"
            :cell-index="index"
            class="cell"
            :winningCell="isWinningCell(index)"
            :game-ended="gameEnded"
            @click="emit('click', index)"
        />
    </div>
</template>

<style scoped>
.board-row {
    background-color: #2b2b2b;
    gap: 2px;
    width: fit-content;
    display: flex;
    flex-direction: row;
    margin: 0 auto;
    overflow-x:clip;
    overflow-y:clip;
    border-radius: 16px;
    box-shadow: inset #272727 4px 4px 4px 4px, inset #272727 -4px -4px 4px 4px;
}

.cell:not(:first-child) {
    margin-left: -1px;
}


</style>