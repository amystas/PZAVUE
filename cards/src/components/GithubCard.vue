<script setup>
import { ref, defineProps, computed } from "vue";
const props = defineProps(['username', 'userData']);
const data = ref({});
const exists = ref(true);

function load() {
    const url = computed(() => 'https://api.github.com/users/' + props.username);
    fetch(url.value)
        .then(response => {
            if (!response.ok) {
                throw new Error('User not found');
            }
            return response.json();
        })
        .then(result => {
            data.value = result;
        })
        .catch(error => {
            exists.value = false;
        });
}

load();

if (props.userData !== undefined && props.userData !== null) {
    data.value = props.userData;
}
</script>

<template>
    <a :href="data.url" target="_blank" v-if="props.userData"
    class="h-[120px] w-[150px] border-solid border-cyan-900 border-4 rounded-xl p-2 bg-sky-100 ml-4 mb-2">
        <img :src="data['avatar_url']" alt="" class="h-[70px] w-[70px] grow-0 shrink-0">
        <h2>{{ data['login'] }}</h2>
    </a>
    <a :href="data.html_url" target="_blank" v-if="props.username && exists" 
    class="w-[350px] border-solid border-cyan-900 border-4 rounded-xl p-4 bg-sky-100 grow-0 shrink-0 m-4">
        <img :src="data['avatar_url']" alt="" class="h-[300px] w-[300px]">
        <h2>{{ data['login'] }}</h2>
        <p>{{ data['name'] }}</p>
        <p>{{ data['bio'] }}</p>
        <p>Lokalizacja: {{ data['location'] }}</p>
        <p>&#x1F465; {{ data['followers'] }} znajomych</p>
    </a>
    <p v-if="!exists && props.username"
    class="border-solid border-red-900 border-4 rounded-xl p-4 bg-red-100 h-16 m-4">
        Nieznaleziono użytkownika {{ props.username }}
    </p>
</template>