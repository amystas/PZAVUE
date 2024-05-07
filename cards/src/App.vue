<script setup>
  import { ref } from 'vue';
  import GithubCardWrapper from "./components/GithubCardWrapper.vue";
  import Search from "./components/Search.vue";
  const users = ref(['amystas', 'teflonn', 'MattMoszczynski', 'sdfgh'])
</script>

<template>
  <GithubCardWrapper :users="users" />
  <Search />
</template>
