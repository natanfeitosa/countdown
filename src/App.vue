<template>
  <Timer :seconds="seconds" />
  <button class="initCounter" @click="handlerCounter">{{ started ? 'Parar' : 'Iniciar' }} contagem</button>
</template>

<script setup lang="ts">
  import { ref, watch, onMounted } from 'vue'
  import Timer from './components/Timer.vue'
  
  const seconds = ref(0)
  const started = ref(false)
  let timeId: number;
  
  watch([started, seconds], ns => {
    if(ns[0]) {
      clearTimeout(timeId as number)
      timeId = setTimeout(() => {
        (seconds.value as number)++
      }, 1000)
      return
    }

    clearTimeout(timeId as number)
  })

  const handlerCounter = () => {
    const counting = started.value
    started.value = !counting

    if(counting) {
      (seconds.value as number)++
    }
  }

</script>

<style>
@import './assets/base.css';

#app {
  width: min(500px, 90%);
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
  border: 1px solid var(--color-border);
  box-shadow: 0 0 10px 4px var(--color-border-hover);

  display: inherit;
  flex-direction: column;
  align-items: center;
}

.initCounter {
  cursor: pointer;
  padding: 0.42rem 1.32rem;
  font-weight: 700;
  font-size: 0.82em;
  width: 56%;

  background-color: var(--color-text);
  color: var(--color-heading);
}
/* @media (min-width: 1024px) {
  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }
} */
</style>
