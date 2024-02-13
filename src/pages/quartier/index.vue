<script setup lang="ts">
import { supabase } from "../../supabase";

// const { data, error } = await supabase.from('QuartierCommune').select(
//   *
// );
const { data, error } = await supabase.from('Quartier').select('Nom, id, Commune(id, Nom)');
if (error) console.log("n'a pas pu charger la table quartier_commune :", error);

</script>

<template>
  <section class="flex flex-col">
    <h3 class="text-2xl">Liste des quartiers</h3>
    <ul>
      <li v-for="quartierObject in (data as any[])">
        {{ quartierObject.Commune.Nom }} -
        {{ quartierObject.Nom }}
      </li>
    </ul>
  </section>

</template>