<script setup lang="ts">
import BlogPost from "@/components/BlogPost.vue";
import {computed, onMounted, ref} from "vue";
import PaginatePost from "@/components/PaginatePost.vue";
import LoadingSpinner from "@/components/LoadingSpinner.vue";

interface BlogPost {
  userId: number,
  id: number,
  title: string,
  body: string
}

const posts = ref<Array<BlogPost>>([])
const postsPerPage = ref<number>(10)
const start = ref<number>(0)
const end = ref<number>(postsPerPage.value)
const loading = ref<boolean>(true)

onMounted(async () => {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts`)
    posts.value = await response.json()
  } catch (e) {
    console.error(e)
  } finally {
    loading.value = false
  }
})

const next = () => {
  start.value += postsPerPage.value
  end.value = start.value + postsPerPage.value
}

const prev = () => {
  start.value -= postsPerPage.value
  end.value = start.value + postsPerPage.value
}

const favorite = ref('')

const changeFavorite = (post: string) => {
  favorite.value = post
}

const maximum = computed(() => posts.value.length)
</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div v-else class="container">
    <h1>APP</h1>
    <PaginatePost
        class="mb-2"
        @next="next"
        @prev="prev"
        :start="start"
        :end="end"
        :maximum="maximum"
    ></PaginatePost>
    <h2>Mis post favorito: {{ favorite }}</h2>
    <BlogPost
        v-for="post in posts.slice(start, end)"
        :title="post.title"
        :key="post.id"
        :id="post.id"
        :body="post.body"
        @changeFavorite="changeFavorite"
        class="mb-2"
    >

    </BlogPost>
  </div>
</template>