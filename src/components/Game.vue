<template>
    <div class="game">
        <game-header :score="score" />
        <game-choices v-if="!userChoice && !computerChoice" @play="play" />
        <game-results
            v-if="userChoice && computerChoice"
            :userChoice="userChoice"
            :computerChoice="computerChoice"
            :result="result"
            @reset="resetGame"
        />
    </div>
</template>

<script setup>
import { ref, onBeforeUnmount } from 'vue';
import GameHeader from '@/components/GameHeader.vue';
import GameChoices from '@/components/GameChoices.vue';
import GameResults from '@/components/GameResults.vue';

const score = ref(parseInt(localStorage.getItem('score')) || 0);
const result = ref('');
const userChoice = ref(null);
const computerChoice = ref(null);

const play = (choice) => {
    const choices = ['rock', 'paper', 'scissors'];
    const computerChoiceValue = choices[Math.floor(Math.random() * choices.length)];

    userChoice.value = choice;
    computerChoice.value = computerChoiceValue;

    if (choice === computerChoiceValue) {
        result.value = 'Ничья!';
    } else if (
        (choice === 'rock' && computerChoiceValue === 'scissors') ||
        (choice === 'paper' && computerChoiceValue === 'rock') ||
        (choice === 'scissors' && computerChoiceValue === 'paper')
    ) {
        result.value = 'Вы победили!';
        score.value++;
    } else {
        result.value = 'Вы проиграли!';
        score.value--;
    }

    saveScore();
};

const saveScore = () => {
    localStorage.setItem('score', score.value);
};

const resetGame = () => {
    userChoice.value = null;
    computerChoice.value = null;
    result.value = '';
};

window.addEventListener('beforeunload', saveScore);

onBeforeUnmount(() => {
    window.removeEventListener('beforeunload', saveScore);
});
</script>

<style scoped>
.game {
    text-align: center;
}

@media (max-width: 600px) {
    .game {
        margin-top: 20px;
    }
}
</style>