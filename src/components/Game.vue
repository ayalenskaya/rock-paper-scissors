<template>
    <div class="game"> 
        <div class="game__body">
            <div v-if="!isBonusGameOpen">
                <game-header :score="score" />
                <game-choices v-if="!userChoice && !computerChoice" @play="play" />
                <game-results v-if="userChoice && computerChoice" :userChoice="userChoice" :computerChoice="computerChoice"
                    :result="result" @reset="resetGame" />
            </div>
        </div>
        <rules-modal :is-open="isRulesModalOpen" @close="closeRulesModal" />
        <bonus-game :is-open="isBonusGameOpen" @close="closeBonusGame" :score="bonusScore" />
        <div class="footer">
            <button class="footer__button" @click="toggleRulesModal">Правила</button>
            <button class="footer__button" @click="toggleBonusGame">
                <template v-if="isBonusGameOpen">Закрыть бонус</template>
                <template v-else>Бонус</template>
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import GameHeader from '@/components/GameHeader.vue';
import GameChoices from '@/components/GameChoices.vue';
import GameResults from '@/components/GameResults.vue';
import RulesModal from '@/components/RulesModal.vue';
import BonusGame from '@/components/BonusGame.vue';

const score = ref(parseInt(localStorage.getItem('score')) || 0);
const bonusScore = ref(parseInt(localStorage.getItem('bonusScore')) || 0);
const result = ref('');
const userChoice = ref(null);
const computerChoice = ref(null);
const isRulesModalOpen = ref(false);
const isBonusGameOpen = ref(false);

const choices = ['paper', 'scissors', 'rock'];

const play = (choice) => {
    const computerChoiceValue = choices[Math.floor(Math.random() * choices.length)];

    userChoice.value = choice;
    computerChoice.value = computerChoiceValue;

    if (userChoice.value === computerChoice.value) {
        result.value = 'Ничья!';
    } else if (
        (userChoice.value === 'paper' && computerChoice.value === 'rock') ||
        (userChoice.value === 'scissors' && computerChoice.value === 'paper') ||
        (userChoice.value === 'rock' && computerChoice.value === 'scissors')
    ) {
        result.value = 'Вы победили!';
        score.value++;
        localStorage.setItem('score', score.value);
    } else {
        result.value = 'Вы проиграли!';
        score.value--;
        localStorage.setItem('score', score.value);
    }
};

const resetGame = () => {
    userChoice.value = null;
    computerChoice.value = null;
    result.value = '';
};

const toggleRulesModal = () => {
    isRulesModalOpen.value = !isRulesModalOpen.value;
};

const closeRulesModal = () => {
    isRulesModalOpen.value = false;
};

const toggleBonusGame = () => {
    isBonusGameOpen.value = !isBonusGameOpen.value;
};

const closeBonusGame = () => {
    isBonusGameOpen.value = false;
};
</script>
  
<style scoped>
.game {
    text-align: center;
}
</style>

<style scoped>
.game {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.footer {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    text-align: center;
    align-items: flex-end;
    gap: 15px;
}

.footer__button {
    width: 200px;
    background-color: inherit;
    color: #fff;
    border: 3px solid;
    border-radius: 10px;
}

@media (max-width: 400px) {
    .game {
        margin-top: 20px;
    }

    .footer {
        justify-content: center;
        align-items: center;
    }
}
</style>