<script setup>
import { computed, provide, toRef } from 'vue';
import { useRoute } from 'vue-router';
import { courses } from '../data/courses';

const route = useRoute();

const course = computed(() =>
  courses.find((c) => c.id === Number(route.params.id))
);

// Пробрасываем данные вкладкам через provide
provide('course', course);

// Для отображения ID в заголовке
const courseId = toRef(() => route.params.id);
</script>

<template>
  <div class="page">
    <template v-if="course">
      <h1>{{ course.title }}</h1>
      <p class="category">Категория: {{ course.category }}</p>

      <nav class="tabs">
        <RouterLink :to="`/courses/${courseId}/description`">Описание</RouterLink>
        <RouterLink :to="`/courses/${courseId}/program`">Программа</RouterLink>
        <RouterLink :to="`/courses/${courseId}/reviews`">Отзывы</RouterLink>
      </nav>

      <hr />

      <RouterView />
    </template>

    <div v-else class="not-found">
      <h2>Курс не найден</h2>
      <p>Возможно, он был удалён или ID указан неверно.</p>
      <RouterLink to="/courses" class="btn">Назад к списку</RouterLink>
    </div>
  </div>
</template>

<style scoped>
.page { padding: 24px; font-family: sans-serif; max-width: 900px; margin: 0 auto; }
.category { color: #666; }
.tabs { display: flex; gap: 8px; margin: 16px 0; }
.tabs a {
  padding: 6px 14px; border: 1px solid #ccc; border-radius: 6px;
  text-decoration: none; color: #333;
}
.tabs a.router-link-active {
  background: #42b883; color: #fff; border-color: #42b883;
}
.not-found { padding: 20px; }
.btn {
  display: inline-block; margin-top: 12px; padding: 8px 16px;
  background: #42b883; color: #fff; text-decoration: none; border-radius: 6px;
}
</style>