<template>
  <v-layout class="rounded rounded-md">
    <v-navigation-drawer>
      <v-list>
        <v-list-item title="训练信息"></v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar title="训练详情">
      <v-btn @click="toggleTheme">更改主题颜色</v-btn>
    </v-app-bar>

    <v-main class="align-center justify-center" style="min-height: 300px;">
      <AppContent></AppContent>
    </v-main>
  </v-layout>
</template>

<script setup>
  import { useTheme } from 'vuetify'
  import AppContent from "./AppContent.vue"
  const theme = useTheme()

  function toggleTheme () {
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
  }
</script>

<style>
</style>
