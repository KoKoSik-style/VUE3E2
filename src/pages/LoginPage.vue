<script setup>
import { ref } from 'vue';
import { useRouter, useRoute } from 'vue-router';

const router = useRouter();
const route = useRoute();

const password = ref('');
const error = ref('');

function login() {
  error.value = '';
  if (password.value === '1234') {
    localStorage.setItem('authToken', 'demo');
    // куда вернуть: query.redirect (из guard) или /dashboard
    const redirect = route.query.redirect || '/dashboard';
    router.push(redirect);
  } else {
    error.value = 'Неверный пароль. Подсказка: 1234';
  }
}
</script>

<template>
  <div class="page">
    <h1>Вход</h1>
    <form @submit.prevent="login" class="form">
      <label>
        Пароль:
        <input v-model="password" type="password" placeholder="Введите пароль" />
      </label>
      <button type="submit" class="btn">Войти</button>
    </form>
    <p v-if="error" class="error">{{ error }}</p>
  </div>
</template>

<style scoped>
.page { padding: 24px; font-family: sans-serif; max-width: 400px; margin: 0 auto; }
.form { display: flex; flex-direction: column; gap: 12px; }
input { padding: 8px; border: 1px solid #ccc; border-radius: 6px; width: 100%; }
.btn {
  padding: 8px 16px; background: #42b883; color: #fff;
  border: none; border-radius: 6px; cursor: pointer;
}
.error { color: #c00; margin-top: 12px; }
</style>