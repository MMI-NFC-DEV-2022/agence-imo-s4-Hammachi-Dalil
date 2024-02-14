<script setup lang="ts">
import { FormKit } from '@formkit/vue';
import { supabase } from "@/supabase";
import { useRouter, useRoute } from 'vue-router/auto';
import { ref} from '@vue/reactivity';
const router = useRouter();
const quartier = ref({});
const route = useRoute('/quartier/edit/[[id]]');

async function upsertQuartier(dataForm, node) {
 const { data, error } = await supabase.from("Quartier").upsert(dataForm).select("id");
 if (error) node.setErrors([error.message])
 else{
    console.log("data :", data);}
    router.push({name:'/quartier/edit/[[id]]', params: {id: data[0].id}});
};


if (route.params.id) {
     //console.log("route.params.id :", route.params.id);
    
    const { data, error } = await supabase.from("Quartier").select("*").eq("id", route.params.id).single();
    //console.log("data :", data);
    
    if (error) console.error("error", error);
    else quartier.value = data;
};

const { data: listeCommune, error } = await supabase
    .from("Commune")
    .select("");
if (error) console.log("n'a pas pu charger la table Commune :", error);
// Les convertir par map en un tableau d'objets {value, label} pour FormKit
const optionsCommune = listeCommune?.map((commune) => ({
    value: commune.id,
    label: commune.Nom,
}));

const { data: listeMaison } = await supabase
    .from("Maison")
    .select("");
// Les convertir par map en un tableau d'objets {value, label} pour FormKit
const optionsMaison = listeMaison?.map((maison) => ({
    value: maison.id,
    label: maison.nomMaison,
}));

</script>

<template>
     <div class="p-2">
<FormKit
        :config="{
                classes: {
                    input: 'p-1 rounded border-gray-300 shadow-sm border',
                    label: 'text-gray-600 italic',
                    outer: 'py-2',
                    
                    },
                }" 
        :submit-attrs="{ 
                        classes: { 
                            input: 'bg-purple-400 p-1 rounded hover:bg-purple-500',
                            
                            } }"
        type="form"
        @submit="upsertQuartier"
        v-model="quartier">
    <FormKit name="Nom" label="Nom du quartier" type="text" />
    <FormKit name="nombre_habitants" type="number" label="Nombre d'habitants"/>
    <FormKit name="maisons" label="maison du quartier" type="select" :options="optionsMaison" />
    <FormKit name="id_Commune" label="commune du quartier" type="select" :options="optionsCommune" />                
</FormKit>


</div>

</template>