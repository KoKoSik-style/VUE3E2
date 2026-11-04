<template>
  <div class="page">
    <h1>Каталог курсов</h1>
    <p>Добро пожаловать! Выберите раздел.</p>
    <RouterLink to="/courses" class="btn">Перейти к курсам</RouterLink>
  </div>
</template>

<style scoped>
.page { padding: 24px; font-family: sans-serif; }
.btn {
  display: inline-block;
  margin-top: 12px;
  padding: 8px 16px;
  background: #42b883;
  color: #fff;
  text-decoration: none;
  border-radius: 6px;
}
</style>