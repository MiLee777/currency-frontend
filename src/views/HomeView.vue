<script setup>
import { ref, onMounted } from 'vue';
import { getCurrency, getHistory } from '@/api/api';
import GetRatesButton from '@/components/GetRatesButton.vue';
import CurrencyRates from '@/components/CurrencyRates.vue';
import HistoryList from '@/components/HistoryList.vue';

const rates = ref(null);
const previousRates = ref(null);
const history = ref([]);
const loading = ref(false);
const error = ref('');

const loadHistory = async () => {
  const res = await getHistory();
  history.value = res.data;
};

const fetchCurrency = async () => {
  try {
    loading.value = true;
    error.value = '';

    const res = await getCurrency();
    rates.value = res.data.today.rates;
    previousRates.value = res.data.previous.rates;

    await loadHistory();
  } catch (e) {
    error.value = 'Не удалось получить курсы. Попробуйте позже';
  } finally {
    loading.value = false;
  }
};

onMounted(() => {
  loadHistory();
});
</script>

<template>
  <div class="container">
    <h1>Курсы валют</h1>

    <GetRatesButton
      :loading="loading"
      @click="fetchCurrency"
    />

    <p v-if="error" class="error">{{ error }}</p>

    <CurrencyRates
      v-if="rates"
      :rates="rates"
      :previousRates="previousRates"
    />

    <HistoryList :history="history" />
  </div>
</template>

<style>
.container {
  max-width: 600px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}

.error {
  color: red;
}
</style>
