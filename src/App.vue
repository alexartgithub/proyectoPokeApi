<script setup>
import {ref} from 'vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
import Paginacion from './components/Paginacion.vue'
import PokemonList from './components/PokemonList.vue';
const pokemons = ref([]);
const cargando = ref(true);
const inicio = ref(0);
const final = ref(5);
const cantidadMuestra = 5;
const favorito = ref(" - ");

fetch('https://pokeapi.co/api/v2/generation/1/')
.then((res)=> res.json())
.then((data) =>{pokemons.value = data.pokemon_species
})
.catch((e)=> console.log(e))
.finally(cargando.value = false);

const elegirFavorito = (name)=>{ favorito.value = name}

const siguiente = ()=>{
  // if(final.value < pokemons.value.length){
    inicio.value += cantidadMuestra;
    final.value += cantidadMuestra;
  // }
}
const anterior = ()=>{
  if(inicio.value > 0){
    inicio.value -= cantidadMuestra;
    final.value -= cantidadMuestra;
  }
}

</script>

<template>
  <div class="container d-flex flex-column">
    <div v-if="cargando === true">
      <LoadingSpinner/>
    </div>
    <div v-else>
      <h1 class="mt-3 mb-4 text-center text-primary">Pokemons de PokeApi</h1>
      <h3>Pokemon elegido : {{ favorito.toUpperCase() }} </h3>
      <Paginacion @siguiente="siguiente" @anterior="anterior" :inicio="inicio" :final="final" :maxLength="pokemons.length"/>
     <PokemonList v-for="pokemon in pokemons.slice(inicio,final)" :key="pokemon.url" :name="pokemon.name" :url="pokemon.url" @elegirFavorito="elegirFavorito"/>
    </div>
  </div>
</template>

<style scoped>

</style>
