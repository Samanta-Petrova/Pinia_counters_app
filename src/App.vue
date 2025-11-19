<script setup>
import {ref, computed} from "vue";

import countersData from "@/assets/counters.js";
import CounterComp from "@/components/CounterComp.vue";
import { useCounterStore } from "@/stores/counter.js";

const store = useCounterStore();

// State
const counters = ref(countersData);

// Funtions
function decrement(id) {
  let curCounter = counters.value.find((counter) => counter.id === id);
  curCounter.count--;
}

function increment(id) {
  let curCounter = counters.value.find((counter) => counter.id === id);
  curCounter.count++;
}

const getSum = computed(() => {
  let sum = 0;
  counters.value.forEach((counter) => (sum += counter.count));
  return sum;
});
</script>

<template>
  <div class="counters">
    <h2>
      Sum of counters: <span>{{store.getSum }}</span>
    </h2>
    <CounterComp v-for="counter in counters" :key="counter.id" :counter="counter"></CounterComp>
  </div>
</template>

<style scoped>
.counters {
  width: 200px;
  margin: 0 auto;
}

h2 {
  text-align: center;
}

h2 span {
  font-size: 3rem;
}
</style>
