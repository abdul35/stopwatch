<script setup lang="ts">
import IconPlus from './components/icons/IconPlus.vue'
import StopWatch from './components/StopWatch.vue'
import { ref } from 'vue'

const stopWatchCount = ref(0)
const createStopWatch = () => {
  ++stopWatchCount.value
}
</script>

<template>
  <div class="wrapper">
    <div class="stopwatch-list">
      <div v-for="item in stopWatchCount" :key="item">
        <StopWatch />
      </div>

      <div @click="createStopWatch" class="create-stopwatch">
        <IconPlus />
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  margin: auto;
  max-width: 95vw;
  padding: 1rem 0;
}
.create-stopwatch {
  width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.stopwatch-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, 225px);
  gap: 25px;
}
</style>
