<script setup>
defineProps({
  loading: Boolean,
});
</script>

<template>
  <button @click="$emit('click')" :disabled="loading">
    {{ loading ? 'Загрузка...' : 'Получить курсы валют' }}
  </button>
</template>

<style>
button {
  padding: 10px 16px;
  font-size: 16px;
  cursor: pointer;
}
button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
</style>
