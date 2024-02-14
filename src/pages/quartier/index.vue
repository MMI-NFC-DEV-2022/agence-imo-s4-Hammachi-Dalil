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
          <li class="m-4 justify-between" v-for="unQuartier in les_quartiers">

            {{ unQuartier.NomQuartier }}
            <RouterLink :to="{ name: '/quartier/edit/[[id]]', params: { id: unQuartier.quartier_id } }"
            class="bg-purple-500 hover:bg-purple-700 text-white font-bold py-1 px-4 rounded m-4">
                Voir
           </RouterLink>
           <RouterLink :to='{name:"/quartier/suppr/[[id]]", params:{id:unQuartier.quartier_id} }' class="text-white font-bold focus-style justify-self-end rounded-md bg-red-500 p-2 shadow-sm m-6 mt-5">
                  Supprimer l'offre
              </RouterLink>
          </li>
        </ul>
      </li>
    </ul>
  </section>

</template>