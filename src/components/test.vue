<script setup>
import { ref, onMounted } from "vue";

const itemRefs = ref([]);

onMounted(() => {
  console.log(itemRefs.value);
});
</script>

<template>
  <ul>
    <li v-for="n in 3" :ref="(el) => itemRefs.push(el)">
      {{ n }}
    </li>
  </ul>
</template>
