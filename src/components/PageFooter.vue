Copyright (c) {{ currentYear }} ATBSPB. Licensed under the MIT License.

<template>
  <footer>
    Copyright &copy; {{ currentYear }} ATBSPB. All rights reserved.
    <br />
    Powered by <a href="https://www.netlify.com" target="_blank">Netlify</a> &amp; <a href="https://zyyo.net/" target="_blank">zyyo</a>
  </footer>
</template>

<script setup>
import { ref } from 'vue'

const currentYear = ref(new Date().getFullYear())
</script>