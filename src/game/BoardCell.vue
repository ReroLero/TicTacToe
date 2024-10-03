<script setup>

//to do 

import {computed} from 'vue'

const props = defineProps({
    variant: {
        type: String,
        required: true
    },
    placement: String, // top, center, bottom
    cellIndex: Number,
    gameEnded: {
        type: Boolean,
        default: false
    },
    winningCell: {
        type: Boolean,
        default: false
    }
})

const emit = defineEmits(['click'])

// COMPUTEDS
const isCellDisabled = computed(() => {
    const isCellFilled = props.variant !== 'empty'
    const isGameEnded = props.gameEnded

    return isCellFilled || isGameEnded
})

const cellBorderRadiusStyle = computed(() => {
    if (props.placement === 'top' && props.cellIndex === 0)
        return 'br-top-left'
    else if(props.placement === 'top' && props.cellIndex === 2)
        return 'br-top-right'
    else if(props.placement === 'bottom' && props.cellIndex === 2)
        return 'br-bottom-right'
    else if(props.placement === 'bottom' && props.cellIndex === 0)
        return 'br-bottom-left'
    else 
        return 'br-all'
})
</script>

<template>
    <button
        :disabled="isCellDisabled"
        :class="cellBorderRadiusStyle"
        @click="emit('click')"
    >
        <div class="buttonContent">
            <span
                class="emptyCell" 
                v-if="variant === 'empty'"
            ></span>
            <span 
                class="nolikCell" 
                :class="{ winningCell }" 
                v-else-if="variant === 'nolik'"
            >
            ⭘
            </span>
            <span 
                class="krestikCell" 
                :class="{ winningCell }" 
                v-else-if="variant === 'krestik'"
            >
            ☓
            </span>
        </div>
    </button>
</template>

<style scoped>

button {
    font-size: 72px;
    width: 144px;
    height: 144px;

    background-color: #3F3F3F;

    display: flex;
    align-items: center;
    justify-content: center;

    padding: 8px 8px;
    border-style: solid;
    border-radius: 16px;
    border-color: #272727;
    cursor: pointer;

    box-shadow: 0 4px 3px 1px #252525, 0 -6px 4px #3f3f3f, inset 0 0 15px 3px #1e1e1e, inset 0 0 30px #3f3f3f;
}


button.br-top-left {border-radius: 20px 0px 0px 0px; }
button.br-top-right {border-radius: 0px 20px 0px 0px}
button.br-bottom-left {border-radius: 0px 0px 0px 20px}
button.br-bottom-right {border-radius: 0px 0px 20px 0px}
button.br-all {border-radius: 0px 0px 0px 0px}

.nolikCell {
    color: #1f1f1f;
    padding-bottom: 12px;
    text-shadow: 1px 1px 6px rgb(36, 36, 36);
}

.krestikCell {
    color: #1f1f1f;
    padding-bottom: 12px;
    text-shadow: 1px 1px 6px rgb(36, 36, 36);
}

.winningCell {
    color: #ffffff;
    text-shadow: 1px 1px 8px rgb(255, 255, 255), 0 0 0.2em rgb(124, 124, 124);
    animation: 2s ease 0s infinite beat;
}

@keyframes beat {
  0%, 50%, 100% { transform: scale(1, 1); }
  30%, 80% { transform: scale(0.95, 0.95); }
}

@keyframes pulse {
  0%, 50%, 100% {  background: transparent; }
  30%, 80% { background: transparent; }
}

.buttonContent {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 104px;
    width: 104px;
    border-radius: 15%;
    background-color: #444444;
    box-shadow:  0 12px 6px 1px #2b2b2b, 0 6px 8px #383838, 0 -12px 6px 1px #333333, 0 -6px 4px #383838, inset 0 0 6px 6px #3F3F3F, inset 0 0 30px #444444;
}

.buttonContent:hover {
    background-color: #444444;
    box-shadow: inset 0 4px 8px 1px #4b4b4b, inset 0 -4px 8px 1px #4b4b4b;
}

.buttonContent:active {
    background-color: #444444;
    box-shadow: inset 0 8px 12px 1px #444444, inset 0 -8px 12px 1px #444444;
    scale: 0.9;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>