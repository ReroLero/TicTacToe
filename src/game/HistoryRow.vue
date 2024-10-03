<script setup>

defineProps({
    move: Object,
    lastMove: Boolean,
})

const emit = defineEmits(['backToMove'])

const TARGET_DICTIONARY = {
    nolik: '⭘',
    krestik: '☓',
}

// METHODS
function onBackToMove(moveId) {
    emit('backToMove', moveId)
}
</script>

<template>
    <div class="historyRow">
        <span class="history-move">{{move.id}}. Player put <span :class="move.target">{{TARGET_DICTIONARY[move.target]}}</span> in the cell {{ move.pos }}</span>
        <div class="cube">
            <button
                v-if="!lastMove"
                class="back-to-move"
                @click="onBackToMove(move.id)"
            >
            <svg
                class="back-to-move__icon"
                width="24"
                height="24" 
                viewBox="0 0 24 24" 
                fill="none" 
                stroke="currentColor"
                xmlns="http://www.w3.org/2000/svg"
            >
                <path 
                    d="M9 15L3 9M3 9L9 3M3 9H15C18.3137 9 21 11.6863 21 15C21 18.3137 18.3137 21 15 21H12"  
                    stroke-width="1.5" 
                    stroke-linecap="round"
                    stroke-linejoin="round" 
                    stroke="currentColor"
                />
            </svg>
            </button>
        </div>
    </div>
</template>

<style scoped>

.back-to-move {
  cursor: pointer;
  border: none;
  background-color: transparent;
  stroke: #ffffff;
  fill: #ffffff;
}

.back-to-move .back-to-move__icon {
    color: #e2e2e2;
}

.back-to-move:hover .back-to-move__icon {
    color:  #ffffff;
}

.history-move {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
}

.historyRow {
    padding: 2px;
    width: 100%;
    height: fit-content;
    display: flex;
    justify-content: space-between;
    flex-direction: row;
    align-items: center;
    height: fit-content;
    font-family: Verdana;
    font-size: 18px;
    color: #ffffff;
}

span.nolik {
    color: #ffffff;
}

span.krestik {
    color: #ffffff;
}


</style>