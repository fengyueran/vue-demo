<script setup lang="ts">
import { ref } from 'vue';
import { nextTick } from 'vue';

import { reactive } from 'vue';

const state = reactive({ count: 0 });

const count = ref(0);
console.log(count); // { value: 0 }
console.log(count.value); // 0

count.value++;
console.log(count.value); // 1

const increment = () => {
  count.value++;
};

const obj = ref({
  nested: { count: 0 },
  arr: ['foo', 'bar']
});

function mutateDeeply() {
  // 以下都会按照期望工作
  obj.value.nested.count++;
  obj.value.arr.push('baz');
}

async function increment1() {
  count.value++;
  await nextTick();
  // 现在 DOM 已经更新了
}
</script>

<template>
  <div>
    <button @click="increment">{{ count }}</button>

    <button @click="mutateDeeply">{{ obj.nested.count }}</button>
    <button @click="state.count++">
      {{ state.count }}
    </button>
  </div>
</template>
<style></style>
