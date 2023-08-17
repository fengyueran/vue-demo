<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);
console.log(count); // { value: 0 }
console.log(count.value); // 0

count.value++;
console.log(count.value); // 1

const increment = () => {
  count.value++;
};

const rawHtml = '<span style="color: red">This should be red.</span>';
const dynamicId = 'id1';
const isButtonDisabled = true;
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper'
};

const date = '2012';

const toTitleDate = (date: string) => {
  return date;
};

const formatDate = (date: string) => {
  return `${date}年`;
};

const attributeName = 'href';
const url = '/test';
const eventName = 'click';

const onSubmit = () => {};
</script>

<template>
  <div>
    <!-- v-html: v-html attribute 被称为一个指令。指令由 v- 作为前缀，
    表明它们是一些由 Vue 提供的特殊 attribute v-html在当前组件实例上，将此元素的 innerHTML 与 rawHtml 属性保持同步 -->
    <p>
      Using text interpolation:
      {{ rawHtml }}
    </p>
    <p>
      Using v-html directive:
      <span v-html="rawHtml"></span>
    </p>

    <!-- v-bind 指令指示 Vue 将元素的 id attribute 与组件的 dynamicId
    属性保持一致。如果绑定的值是 null 或者 undefined，那么该 attribute
    将会从渲染的元素上移除。 -->
    <div v-bind:id="dynamicId"></div>
    <!-- 简写 -->
    <div :id="dynamicId"></div>

    <!-- 当 isButtonDisabled 为真值或一个空字符串 (即 <button disabled="">) 时，
      元素会包含这个 disabled attribute。而当其为其他假值时 attribute 将被忽略。 -->
    <button :disabled="isButtonDisabled">Button</button>

    <!-- 通过不带参数的 v-bind，你可以将它们绑定到单个元素上： -->
    <div v-bind="objectOfAttrs"></div>
    <div>
      <!-- Vue 实际上在所有的数据绑定中都支持完整的 JavaScript 表达式： -->
      {{ isButtonDisabled ? 'YES' : 'NO' }}
      <div :id="`list-${dynamicId}`"></div>
    </div>
    <time :title="toTitleDate(date)" :datetime="date">
      {{ formatDate(date) }}
    </time>

    <!-- 这里，v-if 指令会基于表达式 seen 的值的真假来移除/插入该 <p> 元素。 -->
    <p v-if="isButtonDisabled">Now you see me</p>

    <!-- 另一个例子是 v-on 指令，它将监听 DOM 事件： -->
    <a v-on:click="increment"> ... </a>
    <!-- 这里的参数是要监听的事件名称：click。v-on 有一个相应的缩写，即 @ 字符 -->
    <a @click="increment"> ... </a>

    <!-- 动态参数 -->
    <!-- 注意，参数表达式有一些约束，参见下面“动态参数值的限制”与“动态参数语法的限制”章节的解释 -->
    <a v-bind:[attributeName]="url"> ... </a>
    <!-- 简写 -->
    <a :[attributeName]="url"> ... </a>

    <a v-on:[eventName]="increment"> ... </a>
    <!-- 简写 -->
    <a @[eventName]="increment"></a>

    <!-- 修饰符是以点开头的特殊后缀，表明指令需要以一些特殊的方式被绑定。
      例如 .prevent 修饰符会告知 v-on 指令对触发的事件调用 event.preventDefault()： -->
    <form @submit.prevent="onSubmit">...</form>
  </div>
</template>
<style></style>
