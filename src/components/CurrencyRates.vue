<script setup>
const props = defineProps({
  rates: Object,
  previousRates: Object,
});

const getClass = (currency) => {
  if (!props.previousRates) return 'neutral';

  if (props.rates[currency] > props.previousRates[currency]) return 'up';
  if (props.rates[currency] < props.previousRates[currency]) return 'down';

  return 'neutral';
};
</script>

<template>
  <div class="rates">
    <h2>Текущие курсы</h2>

    <div
      v-for="(value, key) in rates"
      :key="key"
      :class="getClass(key)"
    >
      {{ key }}: {{ value.toFixed(2) }} RUB
    </div>
  </div>
</template>

<style>
.up {
  color: green;
}
.down {
  color: red;
}
.neutral {
  color: gray;
}
</style>
