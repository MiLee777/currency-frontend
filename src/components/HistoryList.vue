<script setup>
defineProps({
  history: Array,
});
</script>

<template>
  <div>
    <h2>История запросов</h2>

    <ul>
      <li v-for="item in history" :key="item._id">
        <div>
          <strong>{{ new Date(item.timestamp).toLocaleString() }}</strong>
        </div>
        <div>IP: {{ item.ip }}</div>
        <div class="rates">
          <div v-for="(value, code) in item.rates" :key="code">
            {{ code }}: {{ value.toFixed(2) }} RUB
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<style>
ul {
  padding: 0;
  list-style: none;
}

li {
  margin-bottom: 12px;
  padding-bottom: 8px;
  border-bottom: 1px solid #ddd;
  display: flex;
  flex-direction: column;
  row-gap: 10px;
}
</style>
