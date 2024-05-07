<script setup>
    import { ref } from 'vue';
    import GithubCardWrapper from "./GithubCardWrapper.vue";
    const search = ref();

    const updateSearch = () => {
        search.value = document.getElementById('newSearch').value;
    };
</script>

<template>
    <div class="ml-4 rounded-xl p-2 bg-lime-100 w-[350px] mb-2">
        <input type="text" id="newSearch" v-on:keyup.enter="updateSearch" 
        class="border-solid border-lime-900 border-2 rounded-3xl p-2 bg-lime-100">
        <button @click="updateSearch" class="ml-4 text-xl">&#x1F50D</button>
    </div>
    <GithubCardWrapper :searchUsers="search"></GithubCardWrapper>
</template>