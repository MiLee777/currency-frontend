<script setup>
import { ref } from 'vue';
import { getCurrency } from '@/api/api';
import GetRatesButton from '@/components/GetRatesButton.vue';
import CurrencyRates from '@/components/CurrencyRates.vue';

const rates = ref(null);
const previousRates = ref(null);
const history = ref([]);
const loading = ref(false);
const error = ref('');

const fetchCurrency = async () => {
  try {
    loading.value = true;
    error.value = '';

    const res = await getCurrency();
    rates.value = res.data.rates;
    previousRates.value = res.data.previous.rates;

  } catch (e) {
    error.value = 'Не удалось получить курсы. Попробуйте позже';
  } finally {
    loading.value = false;
  }
};

</script>

<template>
  <div class="container">
    <h1>Курсы валют</h1>

    <GetRatesButton
      :loading="loading"
      @click="fetchCurrency"
    />

    <CurrencyRates
      v-if="rates"
      :rates="rates"
      :previousRates="previousRates"
    />
  </div>
</template>

<style>
.container {
  max-width: 600px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}
</style>
