<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

function logout() {
  localStorage.removeItem('authToken');
  router.push('/login');
}
</script>

<template>
  <div class="page">
    <h1>Личный кабинет</h1>
    <p>Вы авторизованы.</p>
    <button class="btn" @click="logout">Выйти</button>
  </div>
</template>

<style scoped>
.page { padding: 24px; font-family: sans-serif; max-width: 600px; margin: 0 auto; }
.btn {
  padding: 8px 16px; background: #c0392b; color: #fff;
  border: none; border-radius: 6px; cursor: pointer; margin-top: 12px;
}
</style>