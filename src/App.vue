<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div container>
    <h1>ToDo List</h1>
    <!-- <p><strong>Current route path:</strong> {{ $route.fullPath }}</p> -->
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/login">Login</RouterLink>
      <RouterLink to="/register">Register</RouterLink>
      <RouterLink to="/about">About</RouterLink>
      <RouterLink to="/binding">Binding</RouterLink>
    </nav>

    <main>
      <RouterView />
    </main>
    <footer>
      <p>Copyright 2023</p>
    </footer>
  </div>
</template>

<style scoped></style>
