<template>
  <ChildComp
    ref="child"
    msg="被人遗忘是真正的死亡"
    @change-msg="handleMsg"
    class="child-box"
    title="子组件"
  ></ChildComp>
</template>

<script setup lang="ts">
import ChildComp from "./ChildComp.vue";
import { onMounted, ref } from "vue";

function handleMsg(msg: string) {
  console.log("msg in father: ", msg);
}

// 获取子组件的ref，要同名，ref参数值为null，类型为any
const child = ref<any>(null);
onMounted(() => {
  console.log(child.value.count);
  child.value.increment();
  console.log(child.value.count);
});
</script>
