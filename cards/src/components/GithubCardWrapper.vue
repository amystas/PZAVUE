<script setup>
import { ref, defineProps, computed, watch } from 'vue';
import GithubCard from './GithubCard.vue';
const props = defineProps(['users', 'searchUsers']);
const responseUsers = ref({});

watch(
    () => props.searchUsers,
    async () => {
        responseUsers.value = {};
        const url = computed(() => 'https://api.github.com/search/users?q=' + props.searchUsers);
        fetch(url.value)
        .then(response => response.json())
        .then(result => responseUsers.value = result['items'])
    }
    
)

</script>

<template>
    <div class="flex flex-wrap">
        <GithubCard v-if="props.users" v-for="username in users" :username="username"></GithubCard>
        <GithubCard v-if="props.searchUsers" v-for="data in responseUsers" :userData="data"></GithubCard>
    </div>
</template>