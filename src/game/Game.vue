<script setup>
import ('https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap');
import { ref, computed, watch } from 'vue'
import Greeting from './Greeting.vue'
import Board from './Board.vue'
import History from './History.vue';
import CToast from '../components/CToast.vue';
import CPanel from '../components/CPanel.vue';

// VARIABLES
const isGameStarted = ref(false)

const isToastShow = ref(false)

const winningCells = ref()

const moves = ref([])

// COMPUTEDS
const board = computed(() => getBoardFromMoves())
const isGameEnded = computed(() => !!winningCells.value) 

// WATCHERS
watch(board, () => {
        winningCells.value = getWinningCells()
}, { deep: true })

watch(isGameEnded, (newValue) => {
    const lastMove = (moves.value[moves.value.length - 1])
    if (newValue === true) isToastShow.value=true
})

// METHODS
function isNotEmpty(cell) {
    return cell !== 'empty'
}

function chechTripleCellsForWinning(cells) {
    const isCellsAreNotEmpty = cells.every(c => c !== 'empty')
    const firstCellValue = cells[0]
    const isCellsAreHavesSameValue = cells.every(c => c === firstCellValue)
    
    return isCellsAreNotEmpty && isCellsAreHavesSameValue
}

function getWinningCells() {
    if (chechTripleCellsForWinning([board.value[0][0], board.value[0][1], board.value[0][2]]))
        return ['0:0', '0:1', '0:2']
    if (chechTripleCellsForWinning([board.value[1][0], board.value[1][1], board.value[1][2]]))
        return ['1:0', '1:1', '1:2']
    if (chechTripleCellsForWinning([board.value[2][0], board.value[2][1], board.value[2][2]]))
        return ['2:0', '2:1', '2:2']
    if (chechTripleCellsForWinning([board.value[0][0], board.value[1][0], board.value[2][0]]))
        return ['0:0', '1:0', '2:0']
    if (chechTripleCellsForWinning([board.value[0][1], board.value[1][1], board.value[2][1]]))
        return ['0:1', '1:1', '2:1']
    if (chechTripleCellsForWinning([board.value[0][2], board.value[1][2], board.value[2][2]]))
        return ['0:2', '1:2', '2:2']
    if (chechTripleCellsForWinning([board.value[0][0], board.value[1][1], board.value[2][2]]))
        return ['0:0', '1:1', '2:2']
    if (chechTripleCellsForWinning([board.value[0][2], board.value[1][1], board.value[2][0]]))
        return ['0:2', '1:1', '2:0']

    return undefined
}

function startGame() {
    isGameStarted.value = true
}

function getEmptyBoard() {
    return [
        ['empty', 'empty', 'empty'],
        ['empty', 'empty', 'empty'],
        ['empty', 'empty', 'empty']
    ]
}

function resetGame() {
    moves.value = []
    isToastShow.value=false
}

function onBackToMove(moveId) {
    const index = moves.value.findIndex(m => m.id === moveId)
    moves.value.splice(index + 1, moves.value.length)
}

function getBoardFromMoves() {
    const b = getEmptyBoard()
    for (const moveIndex in moves.value) {
        const { pos } = moves.value[moveIndex]
        const [rowIndex, cellIndex] = pos.split(':')
        b[rowIndex][cellIndex] = moveIndex % 2 === 0 ? 'nolik' : 'krestik'
    }

    return b
}

function onCellClick(event) {
    moves.value.push({
        id: moves.value.length + 1,
        target: moves.value.length % 2 === 0 ? 'nolik' : 'krestik',
        pos: `${event.rowIndex}:${event.cellIndex}`
    })
    
}
</script>

<template>
    <Greeting 
        v-if="!isGameStarted" 
        @start-game="startGame"
    />
    <div v-else class="game">
        <Board 
            :board="board"
            :game-ended="isGameEnded"
            :winning-cells="winningCells"
            @click="onCellClick"
        />
        <History 
            :moves="moves"
            :game-ended="isGameEnded"
            @back-to-move="onBackToMove"
            @reset-game="resetGame"
        />
    </div>
    <Transition>
        <CToast
        v-if="isGameEnded"
         @reset-game="resetGame"/>
    </Transition>
</template>

<style scoped>

/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.75s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.game {
    gap: -22px;
    width: fit-content;
    min-height: fit-content;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
}
</style>