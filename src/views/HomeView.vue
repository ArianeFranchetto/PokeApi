<script setup>
import { onMounted, reactive, ref, computed } from 'vue';
import ListPokemons from "../components/ListPokemons.vue"
import CardPokemonSelected from '../components/CardPokemonSelected.vue';


let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")
let pokemons = reactive(ref());
let searchPokemonField = ref("")
let pokemonSelected = reactive(ref(""));

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then(res => res.json())
    .then(res => pokemons.value = res.results)
})

const pokemonsFiltered = computed(() => {
  if (pokemons.value && searchPokemonField.value) {
    return pokemons.value.filter(pokemon =>
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    )
  }
  return pokemons.value
})

const selectPokemon = async (pokemon) => {
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => pokemonSelected.value = res);
  
}
</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-3">
        <div class="col-sm-12 col-md-6">

          

          <div class="col-sm-15 col-md-15">
            <div class="main" id="card-main">
              <div>
                <div>
                  <div class="mb-3">
                    <div class="section-label">
                      
                    <CardPokemonSelected 
                    :name="pokemonSelected?.name"
                    :xp="pokemonSelected?.base_experience"
                    :id="pokemonSelected?.id"
                    :weight="pokemonSelected?.weight"
                    :img="pokemonSelected?.sprites.other.dream_world.front_default"

                     
              
                 
                     />
                    </div>
                   
                    <input v-model="searchPokemonField" type="text" class="form-control" id="searchPokemonFiel"
                      placeholder="Search Pokemon">
                  </div>
                </div>
                <div id="card-body-poke" class="card-body row">
                  <ListPokemons v-for="pokemon in pokemonsFiltered" :key="pokemon.name" :name="pokemon.name"
                    :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'"
                    @click="selectPokemon(pokemon)" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
#card-main {
  display: flex;
  flex-direction: column;

}


#card-body-poke {
  display: flex;
  justify-content: space-between;

}

.container {
  margin-left: 20%;
  margin-bottom: 7%;


}

.section-label {
  display: flex;
  align-items: center;
 justify-content: center;
 margin-bottom: 15px;

}

#container-img {
  width: 200px;
  margin-left: 3%;
  margin-top: 5px;
  margin-bottom: 8px;

}

h2 {
  color: #fff;
  margin-top: 5px;

}

h2:hover {
  color: rgb(252, 252, 124);
}

.label {
  background: rgb(2, 0, 36);
  background: linear-gradient(90deg, rgba(2, 0, 36, 1) 0%, rgba(9, 41, 121, 1) 48%, rgba(49, 130, 188, 1) 77%, rgba(33, 156, 209, 1) 84%, rgba(0, 212, 255, 1) 100%);
  text-align: center;
  border-radius: 35px;
  margin-bottom: 10px;
}
</style>
