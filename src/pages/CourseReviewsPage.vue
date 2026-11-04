<script setup>
import { inject } from 'vue';
const course = inject('course');
</script>

<template>
  <section>
    <h2>Отзывы</h2>
    <p v-if="course.reviews.length === 0">Пока нет отзывов.</p>
    <ul v-else class="reviews">
      <li v-for="(r, i) in course.reviews" :key="i">
        <strong>{{ r.author }}</strong> — рейтинг: {{ r.rating }}/5
        <p>{{ r.text }}</p>
      </li>
    </ul>
  </section>
</template>

<style scoped>
.reviews { list-style: none; padding: 0; }
.reviews li {
  border: 1px solid #eee; border-radius: 6px;
  padding: 12px; margin-bottom: 8px;
}
</style>