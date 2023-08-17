<script setup lang="ts">
import { ref, reactive, computed } from 'vue';
import TestCss from './TestCss.vue';
import TestCss2 from './TestCss2.vue';

const isActive = ref(true);
const hasError = ref(false);
const classObject = reactive({
  active: true,
  'text-danger': false
});

const activeClass = ref('active');
const errorClass = ref('text-danger');
const activeColor = ref('red');
const fontSize = ref(30);
const styleObject = reactive({
  color: 'red',
  fontSize: '13px'
});
</script>

<template>
  <div
    class="static"
    :class="{ active: isActive, 'text-danger': hasError }"
  ></div>
  <div :class="classObject"></div>
  <div :class="[activeClass, errorClass]"></div>
  <!-- 渲染出的 HTML 为：<p class="foo bar baz boo">Hi!</p> -->
  <TestCss class="baz boo" />
  <!-- 如果你的组件有多个根元素，你将需要指定哪个根元素来接收这个 class。
    你可以通过组件的 $attrs 属性来实现指定： -->
  <TestCss2 class="baz" />

  <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
  <div :style="styleObject"></div>
</template>
