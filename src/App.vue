<template>
  
  <main>
    <div id="word">
      <span v-for="i in state.wordSplitted" class="letter">
        <span>{{ i }}</span>
      </span>
    </div>

    <form @submit.prevent="sendLetter" id="input-letter">
      <input type="text" maxlength="1" v-model="state.letter">
      <button>Enviar</button>
    </form>
    
    <!-- <div id="letters-left">
      <span>a</span>
      <span>b</span>
      <span>c</span>
    </div> -->
  </main>

</template>

<script setup lang="ts">
import { onMounted, reactive } from 'vue';
const word = 'apito';

let state = reactive({
  letter: '' as string,
  wordSplitted: [] as Array<string>,
});

onMounted(() => {
  for (let i = 0; i < word.split('').length; i++) {
    state.wordSplitted.push('');
  }
});

const sendLetter = () => {
  const wordSplitted = new String(word);
  
  for (let i = 0; i < wordSplitted.length; i++) {
    if (state.letter === wordSplitted[i]) {
      state.wordSplitted[i] = state.letter;
    }
  }

  state.letter = '';
}

</script>

<style scoped>
main {
  display: flex;
  flex-direction: column;
}

main #word {
  display: flex;
  justify-content: center;
}

main #word .letter {
  font-size: 4rem;
  padding-left: 1rem;
  padding-right: 1rem;
  display: flex;
  flex-direction: column;
  line-height: 4rem;
  min-width: 5rem;
  justify-content: flex-end;
}

main #word .letter::after {
  content: '';
  border: 1px solid;
  margin: 0;
  padding: 0;
}

main #letters-left {
  border-top: 1px solid rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
}

main #letters-left span {
  font-size: 2rem;
  margin: 2rem;
}

main #word span,
main #letters-left span {
  text-transform: uppercase;
}

#input-letter {
  display: flex;
  justify-content: center;
  padding-top: 5rem;
  padding-bottom: 5rem;
}

#input-letter input {
  border: 1px solid #00897B;
  font-size: 3rem;
  border-right: none;
  text-align: center;
  text-transform: uppercase;
  border-right: none;
}

#input-letter input:focus {
  outline: none;
}

#input-letter button {
  border: 1px solid #00897B;
  cursor: pointer;
  background-color: #00897B;
  color: #FFF;
  font-size: 1rem;
  font-weight: bold;
  padding: 1rem 2rem;
}
</style>
