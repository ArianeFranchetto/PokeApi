<script setup>
import { onMounted, reactive, ref, computed } from 'vue';
import ListPokemons from "../components/ListPokemons.vue"


let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")
let pokemons = reactive(ref());
let searchPokemonField = ref("")

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then(res => res.json())
    .then(res => pokemons.value = res.results)
})

const pokemonsFiltered = computed(()=> {
  if(pokemons.value && searchPokemonField.value){
    return pokemons.value.filter(pokemon => 
    
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
     )
  }
  return pokemons.value
})

</script>

<template>
  <main>
    <div class="container">

      <div class="row mt-3">
        <div class="col-sm-12 col-md-6">
        
          <!-- <div class="card" style="width: 18rem;">
            <img src="https://cdn-icons-png.flaticon.com/512/528/528098.png" class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's
                content.</p>
            </div>

          </div>-->

          <div class="col-sm-15 col-md-15">
            <div class="main" id="card-main">

              <div>
                <div>
                  <div class="mb-3">

                    <section class="label">
                      <img id="container-img"
            src="https://www.pngall.com/wp-content/uploads/13/Pokemon-Logo-PNG-Pic.png"
            class="card-img-top" alt="...">
            <label 
            for="searchPokemonFiel" 
            class="form-label">
            <h2>CHOOSE YOUR POKEMON</h2>
          </label>
                    </section>
                    
                    <input 
                    v-model="searchPokemonField"
                    type="text" 
                    class="form-control" 
                    id="searchPokemonFiel" 
                    placeholder="Search Pokemon"
                    
                    >
                  </div>
                </div>

                <div class="card-body row">
                  <ListPokemons v-for="pokemon in pokemonsFiltered" :key="pokemon.name" :name="pokemon.name"
                    :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'" />

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
  justify-content: space-around;


}

.container {
  margin-left: 27%;
  margin-bottom: 7%;


}

#container-img {
  width: 300px;
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
  background: rgb(2,0,36);
background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(9,41,121,1) 48%, rgba(49,130,188,1) 77%, rgba(33,156,209,1) 84%, rgba(0,212,255,1) 100%);
  text-align: center;
  border-radius: 35px;
  margin-bottom: 10px;
}


</style>
