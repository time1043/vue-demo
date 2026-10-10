<script setup lang="ts">
import { computed, ref, type Ref } from "vue";

const count = ref(1);

// function useDouble<T extends number>(x: Ref<T>) {
//   // return x * 2
//   return computed(() => x.value * 2);
// }

function useDouble<T extends number>(x: Ref<T> | T) {
  // Unify / Generalize: Maybe Ref? Maybe not?
  // manually - isRef(x) ? x.value : x
  // unref(x) - isRef(x) ? x.value : x
  // ref(x) - isRef(x) ? x : ref(x)

  // return computed(() => (isRef(x) ? x.value : x * 2));
  // return computed(() => unref(x) * 2);
  return computed(() => ref(x).value * 2);
}

// const doubled = useDouble(count);
const doubled = useDouble(1);
</script>

<template>
  <h1>{{ count }} x 2 = {{ doubled }}</h1>
  <button @click="count++">Inc</button>
</template>
