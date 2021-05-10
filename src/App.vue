<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon_logo.png" alt="logo pokemon" />
      <hr />
      <h4 class="is-size-4">Pokedex</h4>
      <input
        type="text"
        placeholder="Buscar pokemon pelo nome"
        v-model="busca"
        class="input is-rounded"
      />
      <button
        id="btnBusca"
        class="button is-fullwidth is-success"
        @click="buscar"
      >
        Buscar
      </button>
      <br />
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created: function() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function() {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca.toLowerCase()
        );
      }
    },
  },
  computed: {
    /* resultadoBusca: function() {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca.toLowerCase()
        );
      }
    }, */
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

#btnBusca {
  margin-top: 20px;
}
</style>
