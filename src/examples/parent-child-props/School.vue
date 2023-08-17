<template>
  <Battery :soc="age" />
  <button @click="onClick"></button>
  <div>age{{ age }}</div>
</template>
<style></style>

<script setup lang="ts">
import { ref } from 'vue'
import Battery from './Battery.vue'

// const props = defineProps({
//   value: {
//     type: Number,
//     default: 100
//   }
// })

const age = ref(10)

const onClick = () => {
  age.value += 20
}
</script>
