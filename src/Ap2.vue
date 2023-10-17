<script setup>
import BlogPost from "./components/BlogPost.vue";
import { ref } from 'vue';
const posts = ref([]);
const favPost = ref("");
const changeFav = (title) => {
    favPost.value = title;
}
for (let i = 1; i <= 5; i++) {
    if (i === 3) {
        posts.value.push({
            title: `Post ${i}`,
            body: "",
            colorText: `text-${i % 3 === 0 ? 'danger' : i % 3 === 1 ? 'primary' : 'success'}`
        });
    } else {
        posts.value.push({
            title: `Post ${i}`,
            body: `Desc ${i}`,
            colorText: `text-${i % 3 === 0 ? 'danger' : i % 3 === 1 ? 'primary' : 'success'}`
        });
    }
}
</script>
<template>
    <h1>Vue App</h1>
    <h2>Mi post favorito: {{ favPost }}</h2>
    <blog-post v-for="post in posts" :key="post.id" :post="post" @changeFav="changeFav">
    </blog-post>
</template>