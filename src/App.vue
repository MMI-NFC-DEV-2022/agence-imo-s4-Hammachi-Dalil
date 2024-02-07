<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <h1>header</h1>

    <nav class="*:text-red-500 flex gap-3">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
      <RouterLink to="/list-supabase">Liste-Supabase</RouterLink>
      <RouterLink to="/maisons">Maison</RouterLink>
      <RouterLink to="/connexion">Connexion</RouterLink>
    </nav>
  </header>

  <Suspense>
    <RouterView />
  </Suspense>
  
</template>
