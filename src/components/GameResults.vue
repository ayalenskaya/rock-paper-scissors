<template>
    <div class="game__results" v-if="userChoice && computerChoice">
        <div class="game__result-item">
            <h1 class="game__result-title">Вы выбрали</h1>
            <div class="game__result-image" :class="`game__result-image--${userChoice}`">
                <img :src="userChoiceImage" :alt="`Вы выбрали ${userChoice}`" />
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
                <img :src="computerChoiceImage" :alt="`Компьютер выбрал ${computerChoice}`" />
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
    userChoice: String,
    computerChoice: String,
    result: String
});

const emit = defineEmits(['reset']);

import scissorsImage from '@/assets/scissors.svg';
import paperImage from '@/assets/paper.svg';
import rockImage from '@/assets/rock.svg';
import lizardImage from '@/assets/lizard.svg';
import spockImage from '@/assets/spock.svg';

const imageUrls = {
    scissors: scissorsImage,
    paper: paperImage,
    rock: rockImage,
    lizard: lizardImage,
    spock: spockImage
};

const userChoiceImage = computed(() => imageUrls[props.userChoice]);
const computerChoiceImage = computed(() => imageUrls[props.computerChoice]);
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

.game__result-text {
    margin: 10px 0;
}

.game__play-again-button {
    margin-top: 10px;
    color: blue;
}

@media (max-width: 400px) {

    .game__results {
        flex-direction: column;
        margin-bottom: 20px;
    }

    .game__result-image {
        width: 100px;
        height: 100px;
    }
}
</style>