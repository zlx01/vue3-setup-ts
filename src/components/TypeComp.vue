<template>
  <div>test</div>
</template>

<script setup lang="ts">
import { computed, reactive, ref } from "vue";

type User = {
  name: string;
  age: number;
};

const msg1 = ref("");
const msg2 = ref<string>("");
const user1 = ref<User>({ name: "", age: 0 });
const user2 = ref({} as User);

const obj = reactive({});
const user3 = reactive<User>({ name: "", age: 0 });
const user4 = reactive({} as User);

const msg3 = computed(() => msg1.value.split("").reverse().join(""));
const user5 = computed(() => ({
  name: user1.value.name,
  age: user1.value.age,
}));
</script>
