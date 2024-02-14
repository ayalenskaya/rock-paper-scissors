<template>
    <div class="game__results" v-if="userChoice && computerChoice">
        <div class="game__result-item">
            <h1 class="game__result-title">Вы выбрали</h1>
            <div class="game__result-image" :class="`game__result-image--${userChoice}`">
                <img :src="`src/assets/${userChoice}.svg`" :alt="`Вы выбрали ${userChoice}`" />
            </div>
        </div>
        <div class="game__result-item">
            <span class="game__result-text">
                <p>{{ result }}</p>
            </span>
            <button class="game__play-again-button" v-if="result" @click="$emit('reset')">
                Играть снова
            </button>
        </div>
        <div class="game__result-item">
            <h1 class="game__result-title">Компьютер выбрал</h1>
            <div class="game__result-image" :class="`game__result-image--${computerChoice}`">
                <img :src="`src/assets/${computerChoice}.svg`" :alt="`Компьютер выбрал ${computerChoice}`" />
            </div>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    userChoice: String,
    computerChoice: String,
    result: String
});

const emit = defineEmits(['reset']);
</script>

<style scoped>
.game__results {
    display: flex;
    justify-content: center;
    margin-top: 20px;
    gap: 20px;
}

.game__result-title {
    margin: 20px 0;
    font-size: 20px;
}

.game__result-item {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.game__result-image {
    height: 200px;
    width: 200px; 
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #fff;
    color: #000;
}

.game__result-image--rock {
  border: 20px solid coral;
}

.game__result-image--paper {
    border: 20px solid blue;
}

.game__result-image--scissors {
    border: 20px solid gold;
}
.game__result-text {
    margin: 10px 0;
}

.game__play-again-button {
    margin-top: 10px;
}

@media (max-width: 600px) {
    
    .game__results {
        flex-direction: column;
    }

    .game__result-image {
        width: 100px;
        height: 100px;
    }
}
</style>