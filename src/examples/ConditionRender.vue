<script setup lang="ts">
import { ref, reactive, computed } from 'vue';

const awesome = ref(true);
const type = ref('A');
</script>

<template>
  <button @click="awesome = !awesome">Toggle</button>
  <!-- v-if 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回真值时才被渲染。 -->
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>

  <div v-if="type === 'A'">A</div>
  <div v-else-if="type === 'B'">B</div>
  <div v-else-if="type === 'C'">C</div>
  <div v-else>Not A/B/C</div>
</template>
