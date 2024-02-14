<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <h1>header</h1>

    <nav class="*:text-red-500 flex gap-3 border-orange-950">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
      <RouterLink to="/list-supabase">Liste-Supabase</RouterLink>
      <RouterLink to="/maisons">Maison</RouterLink>
      <RouterLink to="/connexion">Connexion</RouterLink>
      <RouterLink to="/maisons/edit">Edit Maison</RouterLink>
      <RouterLink to="/quartier">Quartier</RouterLink>      
      <RouterLink to="/quartier/edit">Nouveau-quartier</RouterLink>      
      

    </nav>
  </header>

  <Suspense>
    <RouterView />
  </Suspense>
  
</template>
