<script setup lang="ts">
import  AfficheMaison  from '@/components/AfficheMaison.vue';
import { SchemaOfMaison } from '@/type';

const Maisons = [
    {
id: '2',
nomMaison: 'Maison22',
prix: 1234,
favori: true,
image: '',
nbrChambres: 22,
nbrSDB: 22,
adresse: '1234 rue',
surface: '1234',

    },

    {
id: '3',
nomMaison: 'Maison33',
prix: 12345,
favori: true,
image: '',
nbrChambres: 33,
nbrSDB: 33,
adresse: '12345 rue',
surface: '12345',
    },

    {
id: '4',
nomMaison: 'Maison44',
prix: 123456,
favori: true,
image: '',
nbrChambres: 44,
nbrSDB: 44,
adresse: '123456 rue',
surface: '123456',
    }
];

const maMaison :SchemaOfMaison = {
id: '1',
nomMaison: 'Maison11',
prix: 123,
favori: true,
image: '',
nbrChambres: 3,
nbrSDB: 4,
adresse: '123 rue',
surface: '123',

};
</script>

<template>
  <main>Cette page est Index.vue de base</main>
  <AfficheMaison nomMaison="Maison 1" prix="888" />
  <AfficheMaison v-bind="maMaison"/>

  <AfficheMaison v-bind="Maisons[0]"/>
  <AfficheMaison v-bind="Maisons[1]"/>
  <AfficheMaison v-bind="Maisons[2]"/>


</template>
