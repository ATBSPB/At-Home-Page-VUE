<!--
MIT License
Copyright (c) 2026 ATBSPB
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
-->
<template>
  <div>
    <LoadingScreen />
    <div class="at-filter"></div>
    <div class="at-main">
      <LeftSidebar />
      <div class="at-right">
        <PageHeader :theme="theme" @toggle-theme="toggleTheme" />
        <PageContent />
      </div>
    </div>
    <PageFooter />
    <PopupModal />
  </div>
</template>

<script setup>
import { ref, provide, onMounted } from 'vue'
import LoadingScreen from './components/LoadingScreen.vue'
import LeftSidebar from './components/LeftSidebar.vue'
import PageHeader from './components/PageHeader.vue'
import PageContent from './components/PageContent.vue'
import PopupModal from './components/PopupModal.vue'
import PageFooter from './components/PageFooter.vue'
import { getCookie, setCookie } from './utils/cookie.js'

const theme = ref('Light')

function toggleTheme() {
  theme.value = theme.value === 'Dark' ? 'Light' : 'Dark'
  setCookie('themeState', theme.value, 365)
  document.documentElement.dataset.theme = theme.value
}

function applyTheme(t) {
  document.documentElement.dataset.theme = t
  theme.value = t
}

provide('theme', theme)

onMounted(() => {
  const savedTheme = getCookie('themeState') || 'Light'
  applyTheme(savedTheme)

  console.log(
    '%cCopyright © 2026 atbspb.online',
    'background-color: #ff00ff; color: white; font-size: 24px; font-weight: bold; padding: 10px;'
  )
  console.log('%c   /\\_/\\', 'color: #8B4513; font-size: 20px;')
  console.log('%c  ( o.o )', 'color: #8B4513; font-size: 20px;')
  console.log(' %c  > ^ <', 'color: #8B4513; font-size: 20px;')
  console.log('  %c /  ~ \\', 'color: #8B4513; font-size: 20px;')
  console.log('  %c/______\\', 'color: #8B4513; font-size: 20px;')

  document.addEventListener('contextmenu', (event) => {
    event.preventDefault()
  })

  const fpsElement = document.createElement('div')
  fpsElement.id = 'fps'
  fpsElement.style.zIndex = '10000'
  fpsElement.style.position = 'fixed'
  fpsElement.style.left = '0'
  document.body.insertBefore(fpsElement, document.body.firstChild)

  let fps = 0
  let last = Date.now()
  const requestAnimationFrame =
    window.requestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.mozRequestAnimationFrame ||
    window.oRequestAnimationFrame ||
    window.msRequestAnimationFrame ||
    function (callback) {
      window.setTimeout(callback, 1000 / 60)
    }

  function step() {
    const offset = Date.now() - last
    fps += 1
    if (offset >= 1000) {
      last += offset
      fpsElement.textContent = 'FPS: ' + fps
      fps = 0
    }
    requestAnimationFrame(step)
  }
  step()
})
</script>