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
     <div class="footer">
        <button class="footer__button" @click="openRulesModal">Правила</button>
      <rules-modal :is-open="isRulesModalOpen" @close="closeRulesModal" />
      <button class="footer__button">Бонус</button>  
     </div>
      
    </div>
  </template>
  
  <script setup>
  import { ref, onBeforeUnmount } from 'vue';
  import GameHeader from '@/components/GameHeader.vue';
  import GameChoices from '@/components/GameChoices.vue';
  import GameResults from '@/components/GameResults.vue';
  import RulesModal from '@/components/RulesModal.vue';
  
  const score = ref(parseInt(localStorage.getItem('score')) || 0);
  const result = ref('');
  const userChoice = ref(null);
  const computerChoice = ref(null);
  const isRulesModalOpen = ref(false);
  
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
  
  const openRulesModal = () => {
    isRulesModalOpen.value = true;
  };
  
  const closeRulesModal = () => {
    isRulesModalOpen.value = false;
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

@media (max-width: 600px) {
    .game {
        margin-top: 20px;
    }
}
</style>