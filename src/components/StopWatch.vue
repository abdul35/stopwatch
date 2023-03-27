<script setup lang="ts">
import { ref, type Ref } from 'vue'
import IconPause from './icons/IconPause.vue'
import IconTriangle from './icons/IconTriangle.vue'

const WHITE_COLOR = '#ffffff'

let second: Ref<number> = ref(0)
let hour: Ref<number> = ref(0)
let minute: Ref<number> = ref(0)
let ms: Ref<number> = ref(0)
let timer: Ref<number | undefined> = ref()
let isPause: Ref<boolean> = ref(false)
let color: Ref<string> = ref(WHITE_COLOR)

const timerFc = (): void => {
  timer.value = setInterval(() => {
    ms.value += 1

    if (ms.value === 100) {
      second.value += 1
      ms.value = 0
    }

    if (second.value === 60) {
      minute.value += 1
      second.value = 0
    }
    if (minute.value === 60) {
      hour.value += 1
      minute.value = 0
    }
  }, 10)
}

const stopTimer = (): void => {
  clearInterval(timer.value)
}

const controlStopwatch = (): void => {
  if (isPause.value) {
    stopTimer()
    isPause.value = false
    color.value = '#9E9E9E'
  } else {
    timerFc()
    isPause.value = true
    color.value = WHITE_COLOR
  }
}

const clearStopwatch = (): void => {
  second.value = 0
  minute.value = 0
  hour.value = 0
  ms.value = 0
}

const addZero = (num: number): string | number => (num < 10 ? `0${num}` : num)
</script>

<template>
  <div>
    <div class="stopwatch">
      <div :style="{ borderBottomColor: color }" class="stopwatch-header">
        <span :style="{ color }" v-if="hour">{{ addZero(hour) }}:</span>
        <span :style="{ color }" v-if="minute">{{ addZero(minute) }}:</span>
        <span :style="{ color }">{{ addZero(second) }}</span>
      </div>

      <div class="stopwatch-footer">
        <button class="act-button" @click="controlStopwatch">
          <IconTriangle v-if="!isPause" :fillColor="color" />
          <IconPause v-if="isPause" />
        </button>
        <button class="clear" :style="{ backgroundColor: color }" @click="clearStopwatch"></button>
      </div>
    </div>
  </div>
</template>

<style scoped>
@font-face {
  font-family: 'Gotham Pro';
  src: url('../assets/fonts/gothampro_light.ttf') format('truetype');
}
.stopwatch {
  height: 120px;
  width: 225px;
  background-color: #696969;
  display: flex;
  flex-direction: column;
}

.stopwatch-header {
  border-bottom: 1px solid #ffffff;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 22px 0 20px;
}

.stopwatch-header > span {
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  text-align: center;
  color: #ffffff;
  font-family: 'Gotham Pro', serif;
  width: 20px;
  display: inline-table;
}

.stopwatch-footer {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  height: inherit;
}

.act-button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  width: 25px;
}

.clear {
  background-color: #ffffff;
  width: 20px;
  height: 20px;
  border: none;
  cursor: pointer;
  transition: transform 0.1s;
}

.clear:active {
  transform: scale(0.9);
}
</style>
