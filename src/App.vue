<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header class="bg-base-200 shadow-md">
    <div class="navbar container mx-auto">
      <div class="flex-1">
        <a class="btn btn-ghost normal-case text-xl">Form Magistrale</a>
      </div>
      <div class="flex-none">
        <nav class="menu menu-horizontal px-1">
          <RouterLink to="/" class="btn btn-ghost">Home</RouterLink>
          <RouterLink to="/survey" class="btn btn-ghost">Questionario</RouterLink>
        </nav>
      </div>
    </div>
  </header>

  <main class="container mx-auto p-4">
    <RouterView />
  </main>
</template>