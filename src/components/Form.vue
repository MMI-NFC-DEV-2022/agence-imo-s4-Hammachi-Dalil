<script setup lang="ts">
import { ref} from '@vue/reactivity';
import AfficheMaison from '@/components/AfficheMaison.vue';
import { FormKit } from '@formkit/vue';
import type { SchemaOfMaison } from '@/type';
const maison = ref<SchemaOfMaison>({});
import { supabase } from "@/supabase";

async function upsertMaison(dataForm, node) {
 const { data, error } = await supabase.from("Maison").upsert(dataForm).select();
 if (error) node.setErrors([error.message])
}
</script>

<template>
     <div class="p-2">



<FormKit :config="{
                classes: {
                    input: 'p-1 rounded border-gray-300 shadow-sm border',
                    label: 'text-gray-600 italic',
                    outer: 'py-2',
                    },
                }" 
type="form" v-model="maison" @submit="upsertMaison">
    <FormKit name="nomMaison" label="nom" type="text" />
    <FormKit name="prix" label="prix" type="number"/>
    <FormKit name="favori" label="Mettre en valeur" type="checkbox" label-class="pl-2"/>
</FormKit>
</div>
</template>