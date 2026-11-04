<template>
  <div class="page">
    <h1>404 — Страница не найдена</h1>
    <p>Такого адреса не существует.</p>
    <RouterLink to="/" class="btn">На главную</RouterLink>
  </div>
</template>

<style scoped>
.page { padding: 40px; font-family: sans-serif; text-align: center; }
.btn {
  display: inline-block; margin-top: 16px; padding: 8px 16px;
  background: #42b883; color: #fff; text-decoration: none; border-radius: 6px;
}
</style>