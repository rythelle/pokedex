<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo_pokemon.png" />
      <hr />
      <h4 class="is-size-5">Pokedex</h4>
      <input
        class="input is-primary"
        type="text"
        placeholder="Busca Pokemon"
        aria-placeholder="center"
        v-model="search"
        id="inputSearch"
      />
      <button
        class="button is-medium is-fullwidth button is-primary"
        id="searchBtn"
        @click="searchPokemon"
      >
        Buscar
      </button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      search: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    searchPokemon: function () {
      this.filteredPokemons = this.pokemons;
      if (this.search == "" || this.search == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        return (this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.search
        ));
      }
    },
  },
  computed: {
    // resultSearch: function () {
    //   if (this.search == "" || this.search == " ") {
    //     return this.pokemons;
    //   } else {
    //     return this.pokemons.filter((pokemon) => pokemon.name == this.search);
    //   }
    // },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#searchBtn {
  margin-top: 2%;
}
#inputSearch {
  text-align: center;
}
</style>
