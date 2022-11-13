<template>
<h1> {{ name.toLocaleUpperCase()}}</h1>
<h2 :class="classCounter" text-center >{{ counter }}</h2>

<div class="container text-center mt-3">
  <div class="btn-group">
<button @click="increment" class="btn btn-success" >Aumentar</button>
<button @click="desincrement" class="btn btn-danger">Disminuir</button>

<button @click="resetiar" class="btn btn-secundary">resetiar</button>

<button @click="Agregar" :disabled="bloquearBtnbAgregar" class="btn btn-primary">Agregar</button>
</div>

<ul class="list-group mt-4">
  <li 
      class="list-group-item" 
      v-for="(num,index) in arrayFavorito" 
      :key="index">
      {{ num }}
  </li>

</ul>  

</div>


</template>

<script setup>

import {ref, computed} from 'vue'

const name =  "Contador";

const counter = ref(0);

const arrayFavorito = ref([]);

const increment = () => {counter.value ++};
const desincrement = () => {counter.value -- }; 
const resetiar = () => (counter.value = 0);

const Agregar = () => {arrayFavorito.value.push(counter.value);  
}; 

const bloquearBtnbAgregar = computed(() => {
 
  const numSearch = arrayFavorito.value.find((num) => num === counter.value);
   if(numSearch === 0) return true;
  return numSearch ? true : false;
  
});


const classCounter = computed(()=> {
if(counter.value === 0){
  return 'neutro'
}
if(counter.value > 0){
  return 'positive'
}
if(counter.value < 0){
  return 'negative'
}

});


</script>

<style>
h1{
  
  color: #343343;
}

.positive{
  color: green;
}
.negative{
  color: red;
}

.neutro{
  color:black;
}
</style>