<template>
  <div>
    <h1>Kanto Pokédex</h1>
    <ul class="pokemon-table">
      <li
        class="pokemon-list-item"
        v-for="pokemon in pokemonz"
        :key="pokemon.name"
      >
        <PkmnPreview :pokemon="pokemon" />
      </li>
    </ul>
  </div>
</template>

<script>
import PkmnPreview from "./PkmnPreview";
export default {
  name: "PkmnList",
  data() {
    return { pokemonz: [] };
  },
  props: ["id", "offset"],
  created: function () {
    this.fetchData();
  },
  methods: {
    fetchData: async function () {
      try {
        const result = await fetch(
          `https://pokeapi.co/api/v2/pokemon/?limit=${this.id}&offset=${this.offset}`
        );
        const data = await result.json();
        console.log(data);
        this.pokemonz = data.results;
      } catch (error) {
        alert(error);
      }
    },
  },
  components: { PkmnPreview },
};
</script>

<style scoped>
h1 {
  text-transform: uppercase;
  color: #fff;
  font-size: 7rem;
   -webkit-text-stroke: .2rem#111;
   transition: all .3s;
}
h1:hover {
  letter-spacing: .5rem;
}
</style>

