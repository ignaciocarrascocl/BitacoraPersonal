<!-- app.vue -->

<script setup>
import { ref, onMounted } from 'vue';
import { supabase } from '../utils/supabase';

const posts = ref([]);

async function getPosts() {
  const { data } = await supabase.from('posts').select();
  posts.value = data;
}

onMounted(() => {
  getPosts();
});
</script>

<template>
  <h2>Hello! Im supabase.</h2>
  <ul>
    <li v-for="post in posts" :key="post.id">
      <h2>{{ post.title }}</h2>
      <p>{{ post.content }}</p>
      <small
        >Created at: {{ new Date(post.created_at).toLocaleString() }}</small
      >
    </li>
  </ul>
</template>
