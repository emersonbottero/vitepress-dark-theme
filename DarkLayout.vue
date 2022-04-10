<script setup>
import DefaultTheme from 'vitepress/theme'
import { h, compile, onMounted } from 'vue'
const { Layout } = DefaultTheme

onMounted(() => {
  if (
    window.matchMedia &&
    window.matchMedia('(prefers-color-scheme: dark)').matches
  ) {
    console.log('setting as dark')
    document.body.classList.add('dark')
  }

  setTimeout(() => {
    console.log('teste')
    let navBar = document.getElementsByClassName('nav-links')
    if (navBar) {
      navBar = navBar[0]
      console.log(navBar)
      let initial = document.body.classList.contains('dark') ? '🔆' : '🌙'
      console.log('Initial:', initial)
      navBar.insertAdjacentHTML(
        'beforeend',
        `<div class="item" style="padding-left: 8px;" onclick="document.body.classList.toggle('dark'); this.innerHTML= document.body.classList.contains('dark') ? '🔆' : '🌙';"> ${initial} </div>`
      )
    }
  }, 100)
})
</script>

<template>
  <Layout> </Layout>
</template>
