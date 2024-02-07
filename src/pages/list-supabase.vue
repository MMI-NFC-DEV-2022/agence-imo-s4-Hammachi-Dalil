<script setup lang="ts">

import AfficheMaison from '@/components/AfficheMaison.vue';
import { supabase } from "../supabase";
console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code
let { data: data, error } = await supabase
.from('Maison')
.select('*');

const maisons = data ?? []; // à remplacer par l'appel à Supabase
</script>

<template>
    <h1>Liste de la Supabase</h1>
    <AfficheMaison v-for="maison in maisons" v-bind="maison" />
</template>