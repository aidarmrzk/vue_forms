<template>
  <main>
    <FormBuilder v-for="(user, key) in users" :key="key" :user="user"/>
  </main>
</template>

<script setup>
import FormBuilder from '../components/FormBuilder.vue'

import { ref, onMounted } from 'vue'

const users = ref()

onMounted(() => {
  fetchData()
})

const fetchData = () => {
  fetch('form-config.json')
    .then(response => response.json())
    .then(data => {
      users.value = data;
    })
    .catch(error => {
      console.error('Error fetching data:', error);
    });
}
</script>
<style>
body {
  background: linear-gradient(311deg, rgb(25, 33, 46) 0%, rgb(52, 16, 61) 100%);
  color: #fff;
}
main {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 30px;
  margin: 10px 0 0;
  padding: 20px;
}
</style>