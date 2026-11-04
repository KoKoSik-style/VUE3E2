<script setup>
import { inject } from 'vue';
const course = inject('course');
</script>

<template>
  <section>
    <h2>Программа</h2>
    <ol>
      <li v-for="(topic, i) in course.program" :key="i">{{ topic }}</li>
    </ol>
  </section>
</template>