<script setup>
import {ref} from 'vue'
import { useRoute } from 'vue-router';
import axios from 'axios'
import {
  Timeline, TimelineItem, TimelinePoint, TimelineTime, TimelineContent, TimelineTitle
} from 'flowbite-vue'

const route = useRoute()
const postId = route.query.id
const url = `https://mehedipata.com/wp-json/wp/v2/posts/${postId}`
const post = ref({})

async function postDetails(){
    const res = await axios.get(url)
    Object.assign(post.value, res.data)
}

postDetails()
</script>
<template>
<div class="w-full bg-gray-50 border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700">
    <a href="#">
        <img class="h-[400px] w-full" src="https://images.unsplash.com/photo-1682687982046-e5e46906bc6e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80" alt="" />
    </a>
    <div class="p-5">
        <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
            {{ post.title.rendered }}
        </h5>
        <p class="mb-3 font-normal text-gray-800 dark:text-gray-400">
            <span v-html="post.content.rendered"></span>
        </p>

    </div>
</div>
</template>
