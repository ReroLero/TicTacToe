<script setup>
import HistoryRow from './HistoryRow.vue';
import TTButton from './TTButton.vue';
import { computed } from 'vue'

const props = defineProps({
    moves: {
        type: Array,
        required: true
    },
    gameEnded: {
        type: Boolean,
        default: false
    },
})

const emit = defineEmits(['backToMove','resetGame'])

// Когда мы пишем "!!" перед переменной (которая может быть любым типом), она преобразуется в boolean ( преобразует значение (1=1 и тд) в [1, 2, 3, 4..., {}, '123', [], true]=true [0, -1, false, undefined, null]=false)
// COMPUTEDS
const isFirstMove = computed(() => {
    return !!props.moves.length
})

// METHODS
function onBackToMove(moveId) {
    emit('backToMove', moveId)
}

function onResetGame() {
    emit('resetGame')
}
</script>

<template>
    <div class="story">
            <div class="history">
                <div class="bg">
                <img src="../assets/Sdot.svg"
            </div>
        <div class="history-content"> 
                <div class="history-header">
                    <span>History</span>
                </div>
                <div class="history-rows"
                v-if="isFirstMove"
                >
                    <template v-for="(move, index) in moves" :key="move.id">
                    <HistoryRow
                        :last-move="gameEnded === true && moves.length - 1 === index"
                        :move="move"
                        @back-to-move="onBackToMove"
                    />
                    </template>
                </div>
                <div class="history-empty" v-else>
                    <img src="../assets/DivEmpty.svg" alt="Empty">
                </div>
                    <TTButton
                v-if="isFirstMove"
                label="Restart"
                @click="onResetGame"  
                 />
            </div> 
                
        </div>
    </div>
</template>

<style scoped>

.history-rows {
    align-items: end;
    flex-grow: 1;
    height: max-content;
    justify-content: end;
    display: flex;
    flex-direction: column;
    overflow: auto;
}

.story {
    display: flex;
    overflow: hidden;
    height: 454px;
    width: 454px;
    position: relative;
    margin-left: -4px;
    justify-content: center;
    border-radius: 0px 20px 20px 0px;
    padding: 20px;
    background-color: #3F3F3F;
    box-shadow:  inset -1px 0.0015px 3px 0px #3f3f3f, inset 8px 8px 12px 0px #272727, inset -2px -2px 4px 0px #747474;
}

.history-empty {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

 .history {
    position: absolute;
    z-index: 0;
    padding: 20px;
    border-radius: 16px;
    background-color: #1f1f1f;
    gap: 12px;
    justify-content: space-between;
    width: 414px;
    height: 414px;
    display: flex;
    flex-direction: column;
    box-shadow: inset 4px 4px 12px #1b1b1b;
 }

.history-header {
    text-transform: uppercase;
    font-family: fantasy;
    font-size: 20px;
    color: #ffffff;
}
.history-content {
    overflow: hidden;
    gap: 16px;
    position: absolute;
    height: 374px;
    width: 374px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
</style>