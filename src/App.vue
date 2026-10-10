<script setup lang="ts">
import { computed, reactive, ref, type Ref } from "vue";

const count = reactive({ data: 1 });

function useDouble<T extends number>(x: Ref<T> | T) {
  const r = ref(x);
  return computed(() => r.value * 2);
}

// const doubled = useDouble(count.data); // 6 x 2 = 2 ❌
const doubled = useDouble(computed(() => count.data)); // 6 x 2 = 12 ✅
</script>

<template>
  <h1>{{ count.data }} x 2 = {{ doubled }}</h1>
  <button @click="count.data++">Inc</button>
</template>
