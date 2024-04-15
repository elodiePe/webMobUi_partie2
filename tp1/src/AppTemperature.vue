<script setup>
import { ref, defineModel } from 'vue';
import {round} from './utils/math.js';
import BaseInputNumber from './components/BaseInputNumber.vue';
//afin d'éviter les problèmes d'arrondis, nous avons créer une fonction qui arrondi à la deuxième après la virgule (dans la fonction round)
//ref, compute (dépendant d'une ref), model => données réactive
const tempSi = ref(0);
//define model => des compute qui sont sous forme de model
const tempCelsius = defineModel('celsius',{
    get(){
        return tempSi.value-273.15;
    },
    set(value){
tempSi.value = value + 273.15;
    }
});
const tempFaranheit = defineModel('farhenheit',{
    get (){
return tempSi.value*9/5-459.67;
    },
    set(value){
tempSi.value = (value +458.67)*5/9;
    }
});
const tempKelvin = defineModel('kelvin',{
    get (){
return tempSi.value;
    },
    set(value){
tempSi.value = value;
    }
});
</script>

<template>
<div>
    <!-- Champs de saisie pour Kelvin, Celsius et Fahrenheit -->
    <span>{{ tempSi }}</span>
<BaseInputNumber unit="°K" v-model="tempKelvin"/>
<BaseInputNumber unit="°C" v-model="tempCelsius"/>
<BaseInputNumber unit="°F" v-model="tempFaranheit"/>
<!-- <input type="number" v-model="tempSi"> Si on utilise v-model au lieu de :value, il n'y a pas besoin d'appeler un event UNIQUEMENT si la valeur tempSi est une ref. V-model fait automatiquement le 2-way binding -->
    <!-- Affichage des messages -->
    <p v-if="tempKelvin < 0">La température en Kelvin est négative</p>
    <p v-else-if="tempKelvin === 0">La température en kelvin est nulle</p>
    <p v-else>La température en kelvin est positive</p>

</div>
</template>

<style scoped>

</style>