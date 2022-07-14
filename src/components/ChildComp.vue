<template>
  <h1>{{ motto }}</h1>
  <h1>{{ msg }}</h1>
  <button @click="onClick">emit</button>
  <button @click="increment">count is {{ count }}</button>
  <h2>{{ $attrs.title }}</h2>
</template>

<script setup lang="ts">
import type { ListItem } from "@/types/model";
import { ref, useAttrs } from "vue";

const props = withDefaults(
  defineProps<{ msg: string; motto?: string; list?: ListItem[] }>(),
  {
    motto: "Hello World!",
    // 对 object array 需要使用函数
    list: () => [
      { name: "John", age: 30 },
      { name: "Jane", age: 25 },
    ],
  }
);

console.log(props.msg);
console.log(props.list[0].name);

const emits = defineEmits(["changeMsg"]);
function onClick(): void {
  emits("changeMsg", "牧师，我虽然不是上帝的子民，但我能分辨是与非。");
}

const count = ref(100);
function increment(): void {
  count.value++;
}
// 对父组件暴露属性和方法
defineExpose({ count, increment });

const attrs = useAttrs();
console.log(attrs.class);
console.log(attrs.title);
</script>

<script lang="ts">
export default {
  name: "ChildComp",
};
// <script setup> 是没有组件配置项 name 的，可以再使用一个普通的 <script> 来配置 name。
// 两个script必须使用同一种语言，否则会报错
// 每个 *.vue 文件最多可同时包含一个 <script> 块 (不包括<script setup>)；
// 每个 *.vue 文件最多可同时包含一个 <script setup> 块 (不包括常规的 <script>)；
</script>
