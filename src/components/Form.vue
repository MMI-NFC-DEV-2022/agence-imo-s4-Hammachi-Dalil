<script setup lang="ts">
import { ref} from '@vue/reactivity';
import AfficheMaison from '@/components/AfficheMaison.vue';
import { FormKit } from '@formkit/vue';
import type { SchemaOfMaison } from '@/type';
const maison = ref<SchemaOfMaison>({});
import { supabase } from "@/supabase";
import { useRouter, useRoute } from 'vue-router/auto';
const router = useRouter();

async function upsertMaison(dataForm, node) {
 const { data, error } = await supabase.from("Maison").upsert(dataForm).select("id");
 if (error) node.setErrors([error.message])
 else{
    console.log("data :", data);}
    router.push({name:'/maisons/edit/[[id]]', params: {id: data[0].id}});
}

const route = useRoute('/maisons/edit/[[id]]');
if (route.params.id) {
    const { data, error } = await supabase.from("Maison").select("*").eq("id", route.params.id).single();
    if (error) console.error("error", error);
    else maison.value = data;
}

</script>

<template>

<AfficheMaison v-bind="maison" />

     <div class="p-2">
<FormKit :config="{
                classes: {
                    input: 'p-1 rounded border-gray-300 shadow-sm border',
                    label: 'text-gray-600 italic',
                    outer: 'py-2',
                    },
                }" 
type="form" v-model="maison" @submit="upsertMaison">
    <FormKit name="nomMaison" label="Nom" type="text" />
    <FormKit name="prix" label="Prix" type="number"/>
    <FormKit name="favori" label="Mettre en valeur" type="checkbox" label-class="pl-2"/>
    <FormKit name="nbrChambres" label="Nombre de chambres" type="number" label-class="pl-2"/>
    <FormKit name="nbrSDB" label="Nombre de salle de bail" type="number" label-class="pl-2"/>
    <FormKit name="adresse" label="Adresse" type="text" label-class="pl-2"/>
    <FormKit name="surface" label="Surface" type="text" label-class="pl-2"/>

</FormKit>
</div>
</template>