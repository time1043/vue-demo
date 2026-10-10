<script setup lang="ts">
import { computed, reactive, ref, type MaybeRef } from "vue";

const count = reactive({ data: 1 });

// useDouble() is reactive, similar to computed - read-only, no write
// https://github.com/vueuse/vueuse/pull/1743 resolveRef
function useDouble<T extends number>(x: MaybeRef<T> | (() => T)) {
  const r = typeof x === "function" ? computed(x) : ref(x);
  return computed(() => r.value * 2);
}

// const doubled = useDouble(count.data); // 6 x 2 = 2 ❌
// const doubled = useDouble(computed(() => count.data)); // 6 x 2 = 12 ✅
const doubled = useDouble(() => count.data); // Maybe Ref? Maybe not?
</script>

<template>
  <h1>{{ count.data }} x 2 = {{ doubled }}</h1>
  <button @click="count.data++">Inc</button>
</template>
