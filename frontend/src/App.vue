<script setup>
import { RouterLink, RouterView } from 'vue-router'
import logo from "./assets/images/gh-mark.png";
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">
        <img :src="logo" alt="" width="30" height="24" class="d-inline-block align-text-top" />
        GitHub Mona Gallery
      </a>
    </div>
  </nav>

  <RouterView />
</template>

<style scoped></style>
