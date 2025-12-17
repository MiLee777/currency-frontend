<script setup>
import GetRatesButton from '@/components/GetRatesButton.vue';

</script>

<template>
  <div class="container">
    <h1>Курсы валют</h1>

    <GetRatesButton
      :loading="loading"
      @click="fetchCurrency"
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
