<script setup lang="ts">
import { ref } from 'vue'

const onClick = ()=> {
   alert('Click')
}
</script>

<template>
  <button v-on="{ click: onClick }">
    Click
  </button>
</template>
<style></style>
