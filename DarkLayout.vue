<script setup>
import DefaultTheme from 'vitepress/theme'
import ThemeToggle from './ThemeToggle.vue'
const { Layout } = DefaultTheme
</script>

<template>
  <Layout>
    <template #navbar-search>
      <ThemeToggle />
    </template>
  </Layout>
</template>
