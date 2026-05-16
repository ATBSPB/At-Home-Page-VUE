<template>
  <footer>
    At - Home Page &copy; {{ currentYear }} . //
    Powered by <a href="https://www.netlify.com" target="_blank">Netlify</a> &amp; <a href="https://zyyo.net/" target="_blank">zyyo</a>
  </footer>
</template>

<script setup>
import { ref } from 'vue'

const currentYear = ref(new Date().getFullYear())
</script>