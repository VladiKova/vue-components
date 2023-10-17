<script setup>
import { ref } from 'vue';
import BlogPost from "./components/BlogPost.vue";
import PaginatePosts from './components/PaginatePosts.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
const posts = ref([]);
const favPost = ref("");
const increment = 10;
const start = ref(0);
const end = ref(increment);
const loading = ref(false);
const main = ref(false);


//=======FUNCIONES================================
const changeFavPost = (title) => {
    favPost.value = title;
};
const next = () => {
    if (end !== 50) {
        start.value += increment;
        end.value += increment;
    }
};
const previous = () => {
    if (start !== 0) {
        start.value -= increment;
        end.value -= increment;
    }
};
const loadPost = async () => {
    loading.value = true;
    try {
        const res = await fetch('https://jsonplaceholder.typicode.com/posts');
        posts.value = await res.json();

    } catch (error) {
        console.log(error);

    } finally {
        setTimeout(() => {
            loading.value = false;
            main.value = true;
        }, 2000)
    }
}
//======FIN FUNCIONCES================================

</script>
<template>
    <header class="container">
        <button v-show="loading" class="btn btn-outline-info" @click="loadPost" >Load Posts</button>
        <loading-spinner v-if="loading"></loading-spinner>
    </header>

    <main v-show="!loading && main" class="container">
        <h1>APP WITH API</h1>
        <h2>Favorite Post: <b class="text-info">{{ favPost }}</b></h2>
        <paginate-posts class="mb-2 mt-3" :start="start" :end="end" :length="posts.length" @next="next"
            @previous="previous"></paginate-posts>
        <div class="scrollable">
            <blog-post v-for="post in posts.slice(start, end)" :key="post.id" :id="post.id" :title="post.title"
                :body="post.body" @changeFav="changeFavPost" class="mb-2"></blog-post>
        </div>
    </main>
</template>
<style>
.scrollable {
    max-height: 600px;
    overflow-y: auto;
    margin-top: 1%;

}

.scrollable::-webkit-scrollbar {
    width: 12px;
}

.scrollable::-webkit-scrollbar-thumb {
    background-color: rgba(84, 84, 240, 0.76);
    border-radius: 6px;
    margin-bottom: 2%;
}
</style>

