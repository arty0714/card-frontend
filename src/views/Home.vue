<script setup>
import { reactive, ref, watch } from 'vue';

const front = ref(null);
const back = ref(null);
let frontActive = ref(true);

const card = reactive({
    word: 'bike',
    definition: 'велосипед/ровер'
});

function changeSide() {
    frontActive.value = !frontActive.value;
    console.log('changeSide')
}

watch(frontActive, () => {
    console.log(back.value)
    if (frontActive.value) {
        front.value.classList.add('visible')
        back.value.classList.remove('visible')
    } else {
        back.value.classList.add('visible')
        front.value.classList.remove('visible')
    }
    console.log(back.value)
})
</script>
<template>
    <div class="container">
        <div class="card">
            <div ref="front"class="front visible">{{ card.word }}</div>
            <div ref="back" class="back">{{ card.definition }}</div>
        </div>
        <button @click="changeSide">changeSide</button>
    </div>
    
</template>
<style scoped>
.container {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.card {
    min-width: 300px;
    min-height: 200px;
}
.visible {
    visibility: visible !important;
}
.card div {
    visibility: collapse;
}
</style>