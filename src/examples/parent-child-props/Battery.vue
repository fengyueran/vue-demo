<template>
  <div
    class="battery-box"
    :style="{
      '--batteryBodyBaseWidth': batteryBodyBaseWidthWithUnit,
      '--batteryBodyBaseHeight': batteryBodyBaseHeightWithUnit,
      '--batteryCapBaseWidth': batteryCapBaseWidthWithUnit,
      '--batteryCapBaseHeight': batteryCapBaseHeightWithUnit
    }"
  >
    <div class="battery-cap"></div>
    <div class="battery-body" :style="{ borderColor: batteryBodyBorderColor }">
      <div
        class="battery-soc-cell-box"
        v-for="value in [4, 3, 2, 1, 0]"
        :key="value"
        :style="{ opacity: soc1 >= value ? 1 : 0 }"
      >
        <div class="battery-soc-cell"></div>
      </div>
    </div>
    <div>soc: {{ soc }}</div>
    <div>soc1:{{ soc1 }}</div>
  </div>
</template>

<script setup lang="ts">
import { toRefs, watch, ref } from 'vue'
const props = defineProps({
  soc: {
    type: Number,
    default: 100
  },
  batteryBodyBorderColor: {
    type: String,
    default: '#00c5e7'
  }
})

const { batteryBodyBorderColor } = toRefs(props)

const fillPx = (v: number) => ` ${v}px`

const calcSOCLevel = (soc: number) => {
  if (soc <= 0) return -1

  const levels = [20, 40, 60, 80]
  //0-4
  const level = levels.findLastIndex((v) => soc >= v) + 1
  console.log('soc1', level)
  return level
}

const { soc } = toRefs(props)

const soc1 = ref(calcSOCLevel(soc.value))
watch(soc, () => {
  console.log('soc00000', soc.value)

  soc1.value = calcSOCLevel(soc.value)
})

const batteryBodyBaseWidth = 46
const batteryBodyBaseWidthWithUnit = fillPx(batteryBodyBaseWidth)
const batteryBodyBaseHeight = 74
const batteryBodyBaseHeightWithUnit = fillPx(batteryBodyBaseHeight)

const batteryCapBaseWidth = 20
const batteryCapBaseWidthWithUnit = fillPx(batteryCapBaseWidth)
const batteryCapBaseHeight = 7
const batteryCapBaseHeightWithUnit = fillPx(batteryCapBaseHeight)
</script>

<style scoped>
* {
  box-sizing: border-box;
}
.battery-box {
  width: var(--batteryBodyBaseWidth);
  height: var(--batteryBodyBaseHeight);
  display: flex;
  align-items: center;
  flex-direction: column;
}
.battery-cap {
  width: var(--batteryCapBaseWidth);
  height: var(--batteryCapBaseHeight);
  background: #bcedf6;
  opacity: 0.7;
  border-top-left-radius: 2px;
  border-top-right-radius: 2px;
}
.battery-body {
  width: var(--batteryBodyBaseWidth);
  height: var(--batteryBodyBaseHeight);
  border-radius: 6px;
  border: 2px solid #00c5e7;
  padding: 2px 1px;
}
.battery-soc-cell-box {
  width: 100%;
  height: 20%;
  padding: 1px 1px;
  div {
    width: 100%;
    height: 100%;
    background: #00c5e7;
  }
}
</style>
