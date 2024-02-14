<template>
    <div class="game__header">
        <div class="game__header-text">
            <h1 class="game__header-title">rock</h1>
            <h1 class="game__header-title">paper</h1>
            <h1 class="game__header-title">scissors</h1>
        </div>
        <p class="game__score">Счет: <br> {{ score }}</p>
    </div>
</template>

<script setup> 

const props = defineProps({
    score: Number
});
</script>

<style scoped>
.game__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px;
    border: 1px solid;
    border-radius: 20px;
    margin-bottom: 100px;
    width: 500px;
}

.game__header-text {
    text-align: start;
}

.game__header-title {
    margin: 0;
    font-size: 30px;
}

.game__score {
    margin: 0;
    padding: 10px 20px;
    background-color: #fff;
    color: #192042;
    font-size: 30px;
    font-weight: 700;
    border-radius: 20px;
}

@media (max-width: 600px) {
  
    .game__header {
        flex-direction: column;
        width: 100%;
    }

    .game__header-text {
        margin-bottom: 20px;
    }
}
</style>