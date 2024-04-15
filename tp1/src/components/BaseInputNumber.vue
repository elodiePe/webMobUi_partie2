<script setup>
import { round } from '../utils/math.js';
//si on ne veut pas stocker les paramètres, on est pas obligé de mettre const props
const props = defineProps({
    unit:{
        type:String,
        required:false,
    //il est également possible de mettre des vvaleur pas défaut->
        default:false,
},
decimalPlaces:{
type:Number,
required:false,
default:2,
},
});
const model = defineModel({
    get(){
        return round(this.model, props.decimalPlaces);
    },
});
</script>
<template>
    <input type="number" v-model="model">
    <span v-if="unit">{{ unit }}</span> 
    <!-- si il y a une unité -> il affiche -->
</template>
<style scoped>
input{
    display: inline-block;
    margin: 0.5rem 1;

}
</style>