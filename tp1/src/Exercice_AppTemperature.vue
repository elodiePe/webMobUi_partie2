<template>
  <div>
    <!-- Champs de saisie pour Kelvin, Celsius et Fahrenheit -->
    <input type="number" v-model="tempKelvin">
    <input type="number" v-model="tempCelsius" placeholder="Celsius">
    <input type="number" v-model="tempFaranheit" placeholder="Fahrenheit">
<!-- <input type="number" v-model="tempSi"> Si on utilise v-model au lieu de :value, il n'y a pas besoin d'appeler un event UNIQUEMENT si la valeur tempSi est une ref. V-model fait automatiquement le 2-way binding -->
    <!-- Affichage des messages -->
    <p v-if="tempKelvin < 0">La température en Kelvin est négative</p>
    <p v-else-if="tempKelvin === 0">La température est nulle</p>
    <p v-else>La température est positive</p>

  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue';

const tempSi = ref(0);

const tempKelvin = computed({
  get: () => tempSi.value,
  set: (value) => {
    tempSi.value = value;
  }
});

const tempCelsius = computed({
  get: () => tempSi.value - 273.15,
  set: (value) => {
    tempSi.value = value + 273.15;
  }
});

const tempFaranheit = computed({
  get: () => tempSi.value * 9/5 - 459.67,
  set: (value) => {
    tempSi.value = value + 459.67 /9/5;
  }
});
//Le watch permet de suivre des valeurs (ex si une valeur passe en peut loguer qqch)
watch(tempSi, (newtempSi, oldtempSi) => {
  console.log(`Kelvin: ${newtempSi}, Celsius: ${tempCelsius.value}, Fahrenheit: ${tempFaranheit.value}`);
  console.log(`Ancienne valeur : ${oldtempSi}`);
});
</script>

<style>
body {
  background-color: rgb(214, 160, 160);
}
</style>