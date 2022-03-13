<template>
  <div class="timer">
    <span>{{ format(times.hours) }}</span>
    <span class="sep">:</span>
    <span>{{ format(times.minutes) }}</span>
    <span class="sep">:</span>
    <span>{{ format(times.seconds) }}</span>
  </div>
</template>

<script lang="ts" setup>
  import { toRef, toRefs, reactive, watch } from 'vue'
  const props = defineProps({ seconds: Number })
  const s = toRef(props, 'seconds')

  const times = toRefs(reactive({seconds: 0, minutes: 0, hours: 0}))
  
  watch(props, () => {
    let seconds = s.value + 0
    let hours = Math.floor(seconds / 60 ** 2)
    seconds -= hours * 60 ** 2
    let minutes = Math.floor(seconds / 60)
    seconds = Math.floor(seconds % 60)

    Object.assign(times, { seconds, minutes, hours })
  })

  const format = v => {
    if(isNaN(v)) {
      v = 0
    }
    return v.toString().padStart(2, 0)
  }
</script>

<style scoped>
  * {
    font-family: 'Edit Undo Line BRK';
    font-size: 1.82em;
  }

  @media (min-width: 375px) {
    * {
      font-size: 1.96em;
    }
  }

  @media (min-width: 400px) {
    * {
      font-size: 2em;
    }
  }

  @media (min-width: 475px) {
    * {
      font-size: 2.26em;
    }
  }

  @media (min-width: 600px) {
    * {
      font-size: 2.56em;
    }
  }

  .timer {
    /* width: 90%; */
    text-align: center;
    /* margin: auto; */
  }

  .sep {
    padding: 0 .08em;
  }
</style>