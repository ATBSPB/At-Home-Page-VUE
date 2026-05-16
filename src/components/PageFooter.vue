<template>
  <footer>
    At - Home Page &copy; {{ currentYear }} . //
    Powered by <a href="https://vuejs.org/" target="_blank">Vue</a> &amp; <a href="https://www.netlify.com" target="_blank">Netlify</a>
  </footer>
</template>

<script setup>
import { ref } from 'vue'

const currentYear = ref(new Date().getFullYear())
</script>