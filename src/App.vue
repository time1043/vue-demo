<script setup lang="ts">
import { computed, ref, type Ref } from "vue";

const count = ref(1);

function useDouble<T extends number>(x: Ref<T>) {
  // return x * 2
  return computed(() => x.value * 2);
}

const doubled = useDouble(count);
</script>

<template>
  <h1>{{ count }} x 2 = {{ doubled }}</h1>
  <button @click="count++">Inc</button>
</template>
