<script setup lang="ts">
import { ref} from '@vue/reactivity';
import AfficheMaison from '@/components/AfficheMaison.vue';
import { FormKit } from '@formkit/vue';
import type { SchemaOfMaison } from '@/type';
import Form from "@/components/Form.vue";
const maison = ref<SchemaOfMaison>({});
import { supabase } from "@/supabase";

async function upsertMaison(dataForm, node) {
 const { data, error } = await supabase.from("Maison").upsert(dataForm);
 if (error) node.setErrors([error.message])
}

</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat (prévisualisation)</h2>
            <AfficheMaison v-bind="maison" />
        </div>
    </div>
    <Form />
</template>