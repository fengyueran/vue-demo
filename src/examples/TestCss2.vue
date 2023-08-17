<script setup lang="ts"></script>

<template>
  <!-- MyComponent 模板使用 $attrs 时 -->
  <p :class="$attrs.class">Hi!</p>
  <span>This is a child component</span>
</template>
