<script setup>
import { ref, computed, onMounted, watch } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { courses } from '../data/courses';

const route = useRoute();
const router = useRouter();

const loading = ref(true);
const error = ref(null);
const allCourses = ref([]);

// Имитация загрузки с бэкенда
async function fetchCourses() {
  loading.value = true;
  error.value = null;
  try {
    await new Promise((res) => setTimeout(res, 1000));
    allCourses.value = courses;
  } catch (e) {
    error.value = 'Не удалось загрузить курсы';
  } finally {
    loading.value = false;
  }
}

onMounted(fetchCourses);

// Текущая категория из query
const currentCategory = computed(() => route.query.category || 'all');

const filteredCourses = computed(() => {
  if (currentCategory.value === 'all') return allCourses.value;
  return allCourses.value.filter((c) => c.category === currentCategory.value);
});

function setCategory(cat) {
  router.push({
    path: '/courses',
    query: cat === 'all' ? {} : { category: cat },
  });
}

// если пользователь меняет query руками — ничего дополнительно не нужно,
// computed пересчитается автоматически
</script>

<template>
  <div class="page">
    <h1>Курсы</h1>

    <div class="filters">
      <button
        :class="{ active: currentCategory === 'all' }"
        @click="setCategory('all')"
      >
        Все
      </button>
      <button
        :class="{ active: currentCategory === 'frontend' }"
        @click="setCategory('frontend')"
      >
        Frontend
      </button>
      <button
        :class="{ active: currentCategory === 'backend' }"
        @click="setCategory('backend')"
      >
        Backend
      </button>
    </div>

    <div v-if="loading" class="spinner-wrap">
      <div class="spinner"></div>
      <p>Загрузка курсов…</p>
    </div>

    <div v-else-if="error" class="error">
      {{ error }}
      <button @click="fetchCourses">Повторить</button>
    </div>

    <div v-else-if="filteredCourses.length === 0" class="empty">
      Курсов в этой категории нет.
    </div>

    <ul v-else class="cards">
      <li v-for="course in filteredCourses" :key="course.id" class="card">
        <h3>{{ course.title }}</h3>
        <span class="category">{{ course.category }}</span>
        <RouterLink :to="`/courses/${course.id}`" class="btn">
          Подробнее
        </RouterLink>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.page { padding: 24px; font-family: sans-serif; max-width: 900px; margin: 0 auto; }
.filters { display: flex; gap: 8px; margin: 16px 0; }
.filters button {
  padding: 6px 14px; border: 1px solid #ccc; background: #fff;
  border-radius: 6px; cursor: pointer;
}
.filters button.active { background: #42b883; color: #fff; border-color: #42b883; }
.cards { list-style: none; padding: 0; display: grid; gap: 12px; }
.card {
  border: 1px solid #eee; border-radius: 8px; padding: 16px;
  display: flex; align-items: center; gap: 12px; flex-wrap: wrap;
}
.card h3 { margin: 0; flex: 1 1 200px; }
.category {
  background: #eef; padding: 2px 8px; border-radius: 4px; font-size: 13px;
}
.btn {
  padding: 6px 12px; background: #42b883; color: #fff;
  text-decoration: none; border-radius: 6px; font-size: 14px;
}
.spinner-wrap { text-align: center; padding: 40px; }
.spinner {
  width: 36px; height: 36px; margin: 0 auto 12px;
  border: 4px solid #eee; border-top-color: #42b883;
  border-radius: 50%; animation: spin 0.8s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
.error { color: #c00; padding: 20px; }
.empty { padding: 20px; color: #666; }
</style>