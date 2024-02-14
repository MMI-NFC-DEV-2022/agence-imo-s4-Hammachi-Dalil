<script setup lang="ts">
import { supabase } from "../../supabase";

 const { data, error } = await supabase.from('quartiercommune').select();

//const { data, error } = await supabase.from('Quartier').select('Nom, id, Commune(id, Nom)');
if (error) console.log("n'a pas pu charger la table quartier_commune :", error);



const group=  Object.groupBy(data, v=>v.NomCommune)
console.log("group :", group);
</script>

<template>
  <section class="flex flex-col">
    <h3 class="text-2xl">Liste des quartiers</h3>
    <ul>
      <li v-for="(les_quartiers, NomCommune) in group">
        <!-- {{ quartierObject.Commune.Nom }} -
        {{ quartierObject.Nom }} -->
        <h1 class="font-bold mt-3vh text-purple-800">{{ NomCommune }}</h1>
        <ul>
          <li class="ml-10" v-for="quartierObject in les_quartiers">
            {{ quartierObject.NomQuartier }}
            <RouterLink :to="{ name: '/quartier/edit/[[id]]', params: { id: quartierObject.id } }">
              <button class="bg-purple-500 hover:bg-purple-700 text-white font-bold py-1 px-4 rounded m-4">
                Voir
              </button> </RouterLink>
          </li>
        </ul>
      </li>
    </ul>
  </section>

</template>