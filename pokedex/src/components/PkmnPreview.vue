<template>
  <router-link :to="pkmnPath" class="link">
    <div class="pkmn-container">
      <h2>#{{ singlePokemon.id }}</h2>
      <h1 id="query">{{ pokemon.name }}</h1>
      <img :src="sprite" alt="pokemon image" />
    </div>
  </router-link>
</template>

<script>
export default {
  name: "PkmnPreview",
  props: ["pokemon"],
  data() {
    return {
      singlePokemon: {},
    };
  },
  mounted: function () {
    this.fetchData();
    console.log(this.singlePokemon);
  },
  methods: {
    fetchData: async function () {
      try {
        const result = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${this.pokemon.name}`
        );
        const singlePokemon = await result.json();
        this.singlePokemon = singlePokemon;
      } catch (error) {
        alert(error);
      }
    },
  },
  computed: {
    sprite: function () {
      //return this.singlePokemon.sprites.front_default;
      return `https://pokeres.bastionbot.org/images/pokemon/${this.singlePokemon.id}.png`;
    },
    pkmnPath: function () {
      return `/pkmn/${this.singlePokemon.id}`;
    },
  },
};
</script>

<style scoped>
#query {
  color: #111;
  font-size: 2rem;
  margin-bottom: 1rem;
  display: inline;
}
.pkmn-container {
  background-color: #fff;
  padding: 2rem;
  color: #111;
  border: #333 0.3rem solid;
  border-radius: 1rem;
}
h2 {
  font-size: 2rem;
  font-weight: 300;
  text-align: left;
  display: inline;
  margin-right: 2rem;
}
</style>
