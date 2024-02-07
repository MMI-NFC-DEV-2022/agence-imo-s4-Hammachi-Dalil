<script setup lang="ts">
import { ref} from '@vue/reactivity';
import AfficheMaison from '@/components/AfficheMaison.vue';
import { FormKit } from '@formkit/vue';
import type { SchemaOfMaison } from '@/type';
const maison = ref<SchemaOfMaison>({});
</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat (prévisualisation)</h2>
            <AfficheMaison v-bind="maison" />
        </div>
    <div class="p-2">



        <FormKit :config="{
                        classes: {
                            input: 'p-1 rounded border-gray-300 shadow-sm border',
                            label: 'text-gray-600 italic',
                            outer: 'py-2',
                            },
                        }" 
        type="form" v-model="maison">
            <FormKit name="nomMaison" label="nom" type="text" />
            <FormKit name="prix" label="prix" type="number"/>
            <FormKit name="favori" label="Mettre en valeur" type="checkbox" label-class="pl-2"/>
        </FormKit>
        </div>
    </div>
</template>