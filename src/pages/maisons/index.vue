<script setup lang="ts">
import  AfficheMaison  from '@/components/AfficheMaison.vue';
import { SchemaOfMaison } from '@/type';
import { supabase } from "@/supabase";

console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code
let { data: data, error } = await supabase
    .from('Maison')
    .select('*');




const tableauMaison = data ?? [];
</script>

<template>
  <main>Cette page est index.vue de Maison </main>
  <div class="margin-auto justify-center">  
    <AfficheMaison v-for="maison in tableauMaison" v-bind="maison" style="margin: 3vh; display: flex;"   />
  </div>
</template>