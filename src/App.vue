<!--Estructura Simple File Component-->

<script setup>
  import {ref, computed} from 'vue';

  const name = 'Vue dinámico';
  const stylecolor = 'color: blue';
  const arrayColores = ["yellow", "red", "green"];
  const activo = true;
  const showElement = true;
  const arrayFrutas = ["🍉", "🍒", "🍓", "🍌"];
  const arrayDetalleFrutas = [
    {
      name: "Manzanas",
      price: "$300",
      description: "Un kilo de manzanas",
      image: "🍎",
    },
    {
      name: "Peras",
      price: "$350",
      description: "Un kilo de peras",
      image: "🍐",
    },
    {
      name: "Naranjas",
      price: "$200",
      description: "Un kilo de naranjas",
      image: "🍊"
    }
  ];

  const objetoFruta =     {
      name: "Uva",
      price: "$260",
      description: "Un kilo de uvas",
      image: "🍇"
  };

  const arrayStockFrutas = [
  {
    id:1,
    name: "Manzana",
    price: "$300",
    description: "Un kilo de manzanas",
    image: "🍎",
    stock: 0
  },
  {
    id:2,
    name: "Pera",
    price: "$350",
    description: "Un kilo de peras",
    image: "🍐",
    stock: 10
  },
  {
    id:3,
    name: "Naranja",
    price: "$200",
    description: "Un kilo de naranjas",
    image: "🍊",
    stock: 2
  },
  {
    id:4,
    name: "Uva",
    price: "$260",
    description: "Un kilo de uvas",
    image: "🍇",
    stock: 0
  }
];

//Metodos

const handleClick = () =>{
  console.log("Me hiciste click")
}

const contador = ref(0);
const arrayFavoritos = ref([]);

const increment = () =>{
  contador.value ++;
}

const disminuir = () =>{
  contador.value --;
}

const reiniciar = () =>{
  contador.value = 0;
}

const favorito = () =>{
  arrayFavoritos.value.push(contador.value)
}

const classFavorito = computed(()=>{
  const buscarNum = arrayFavoritos.value.find(num => num === contador.value)
  if(buscarNum === 0) return true; 
  return buscarNum ? true : false
})

const classCounter = computed(()=>{
  if(contador.value === 0){
    return 'zero';
  }
  if(contador.value > 0){
    return 'positive';
  }
  if(contador.value < 0){
    return 'negative';
  }
})
</script>

<template>
  <div class="container mx-auto">
    <h1>Hola {{ name.toLocaleUpperCase() }}</h1>
  <br>
  <h2>{{ arrayColores }}</h2>
  <br>
  <h2 :style="`color: ${arrayColores[1]}`">Soy Rojo</h2>
  <br>
  <!--Se puede usar {{ activo ? 'Estoy activo' : 'Estoy inactivo' }}  o v-if-->
  <h2 v-if="activo === true">Estoy activo</h2>

  <!--Directivas v-else-if-->
  <h2 v-else-if="activo === false">Estoy inactivo</h2>

  <!--Directivas v-else-->
  <h2 v-else>Estoy indeciso</h2>

  <br>
  <!--Directivas v-show Agrega o quita Display none al elemento-->
  <h2 v-show="showElement">Show</h2>

  <!--Directivas v-for="elemento in arrayElement" Se puede usar In o Of-->
  <ul class="list-group">
    <li class="list-group-item" v-for="fruta in arrayFrutas">
      {{ fruta }}
    </li>

    <!-- Tambien podemos ponerle el index:
    <li v-for="(fruta, index) in arrayFrutas":key="index">
      {{ index }} - {{ fruta }}
    </li>-->
  </ul>
  <br>
    
  <hr>
  <h1>Frutas Array</h1>
  <ul class="list-group">
    <li class="list-group-item" v-for="detalleFruta in arrayDetalleFrutas" :key="detalleFruta.name">
      {{ detalleFruta.name }} {{ detalleFruta.image }} <br>
      Precio: {{ detalleFruta.price }} <br>
      Descripción: {{ detalleFruta.description }}
      <br>
      <br>
    </li>
  </ul>
  <br>

  <hr>
  <!--V-for para recorrer Objetos-->
  <h1>Objeto Fruta (v-for para recorrer Objetos)</h1>
  <br>
  <ul class="list-group">
    <li class="list-group-item" v-for="(value, propiedad, index) in objetoFruta" :key="value">
      {{ index }} - {{ propiedad }}: {{ value }}
    </li>
  </ul>
  <br>

  <hr>
  <!--v-if dentro de v-for-->
  <h1>Stock Frutas (v-if dentro de v-for)</h1>
  <br>
  <ul class="list-group">
    <template v-for="stockFrutas in arrayStockFrutas" :key="stockFrutas.id">
      <li class="list-group-item" v-if="stockFrutas.stock > 0">
        {{ stockFrutas.image }} {{ stockFrutas.name }} {{ stockFrutas.price }}
      </li>
    </template>
  </ul>
  <br>

  <hr>
  <!--v-on-->
  <h1>V-on acortado con @</h1>
  <br>
  <button v-on:click="handleClick('Texto 1')" class="btn btn-light rounded-5 m-2">Activame 1</button>
  <br>
  <!-- v-on simplificado: @-->
  <button @click="handleClick" class="btn btn-light rounded-5 m-2">Activame 2</button>
  
  <br>
  
  <div>
    <button @click.right.prevent="handleClick('Texto Right')" class="btn btn-primary rounded-5 m-2">Activame right</button>
    <button @click.left="handleClick('Texto Left')" class="btn btn-secondary rounded-5 m-2">Activame left</button>
    <button @click.middle="handleClick('Texto Middle')" class="btn btn-info rounded-5 m-2">Activame middle</button>
  </div>

  <hr>
  <!-- ref() referencia reactiva-->
  <br>
  <h1>Contador (ref())</h1>
  <div class="text-center">
      <br>
      <!-- Forma simple
      <h2 v-if="contador > 0">
        <span :style="`color: green`">{{ contador }}</span>
      </h2>
      <h2 v-if="contador < 0">
        <span :style="`color: red`">{{ contador }}</span>
      </h2>
      <h2 v-if="contador === 0">
        <span :style="`color: white`">{{ contador }}</span>
      </h2> -->

      <!--Otra forma con Clases Dinamicas
        <h2 :class="contador > 0 ? 'positive' : 'negative' ">
          {{ contador }}
        </h2>-->
      

      <!--Computed (propiedades computados)-->
      <!--Otra forma con Computed-->
        <h2 :class="classCounter">{{ contador }}</h2>
        <h3>Favoritos</h3>
        <ul class="list-group">
          <li class="list-group-item" v-for="numeroFav in arrayFavoritos" :key="numeroFav">
            {{ numeroFav }}
          </li>
        </ul>
      

      <br>
      <button @click="increment" class="btn btn-success rounded-5 m-2">Aumentar</button>
      <button @click="disminuir" class="btn btn-danger rounded-5 m-2">Disminuir</button>
      <button @click="reiniciar" class="btn btn-primary rounded-5 m-2">Reiniciar</button>
      <button @click="favorito" :disabled="classFavorito" class="btn btn-warning rounded-5 m-2">Agregar a Favorito</button>
    </div>
  </div>
  




</template>


<style> 
  h1{
    color: rgb(246, 55, 148);
  }
  body{
    padding: 100px;
  }
  .positive{
    color: green
  }
  .negative{
    color: red
  }
  .zero{
    color: white
  }
</style>