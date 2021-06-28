<template>
    <div class="container">
        <div :style="backgroundColor" v-tilt="{ speed: 2000, perspective: 1000, glare: true }" class="poke-card">
            <h2 :style="textColor">{{ singlePokemon.name }}</h2>
            <img :src="sprite" alt="">
            <h3 :style="textColor">{{ singlePokemon.types[0].type.name }}</h3>
            <ul class="poke-stats">
                <li v-for="stat in stats" :key="stat" class="poke-stat">
                    <div :style="textColor">{{ stat.stat.name }}</div>
                    <div :style="textColor">{{ stat.base_stat }}</div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            singlePokemon: {},
            stats: [],
            typeColor: "",
            colors: {
                fire: "#FD7D24",
                grass: "#9BCC50",
                electric: "#EED535",
                water: "#4592C4",
                ground: "#A38C21",
                rock: "#A38C21",
                fairy: "#FDB9E9",
                poison: "#B97FC9",
                ghost: "#B97FC9",
                bug: "#729F3F",
                dragon: "#7766EE",
                psychic: "#F366B9",
                flying: "#BDB9B8",
                fighting: "#D56723",
                normal: "#999",
                ice: "#51C4E7",
                steel: "#AAAABB",
                dark: "#775544",
            },
        };
    },
    computed: {
        sprite: function() {
        return `https://pokeres.bastionbot.org/images/pokemon/${this.singlePokemon.id}.png`
        },
        backgroundColor: function() {
            return "background-color: " + this.colors[`${this.typeColor}`];
        },
        textColor: function() {
            return "color: " + this.colors[`${this.typeColor}`];
        },
    },
    created: function () {
        this.fetchData();
    },
    methods: {
        fetchData: async function () {
      try {
        const result = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${this.$route.params.id}`
        );
        const singlePokemon = await result.json();
        this.singlePokemon = singlePokemon;
        this.stats = singlePokemon.stats;
        this.typeColor = this.singlePokemon.types[0].type.name;
      } catch (error) {
          alert(error);
      }
    },
    }
};
</script>


<style scoped>
body {
  background-color: #e43a3a;
}
.container {
  background-color: #e43a3a;
  height: 100vh;
  width: 100vw;
}
h2 {
  -webkit-text-stroke: .3rem #fff;
  font-size: 4rem;
  text-transform: uppercase;
  transform: translateZ(9rem);
  letter-spacing: .2rem;
}
h3 {
  font-size: 2.5rem;
  text-transform: uppercase;
  padding: 2rem 4rem;
  transform: translateZ(7rem);
  color: #fff;
  border-radius: 1.5rem;
  background-color: #fff;
}
.poke-card {
  transform-style: preserve-3d;
  box-shadow: 0 0 3rem 1rem rgba(255, 252, 80, .8);
  border: #333 0.3rem solid;
  padding: 2rem;
  width: 35vw;
  margin: 10rem auto;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  border-radius: 2rem;
}
img {
  margin: 1rem auto;
  width: 20rem;
   transform: translateZ(8rem);
}
/* li:nth-of-type(1) {
  grid-area: HP;
}
li:nth-of-type(2) {
  grid-area: Attack;
}
li:nth-of-type(3) {
  grid-area: Defense;
}
li:nth-of-type(4) {
  grid-area: spattack;
}
li:nth-of-type(5) {
  grid-area: spedefense;
}
li:nth-of-type(6) {
  grid-area: speed;
}
 */
.poke-stats {
  background-color: #fff;
  padding: 1rem;
  margin: 2rem auto;
  border-radius: 1.75rem;
  text-transform: uppercase;
  transform: translateZ(2rem);
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: 80%;
  place-items: center;
  gap: 2rem;
  transform: translateZ(10rem);
}
.poke-stat {
  text-transform: uppercase;
  font-size: 1.6rem;
  font-weight: 800;
  /* width: 40%; */
  list-style: none;
  width: 100%;
}
.poke-stat div {
  padding: .5rem;
  transform: translateZ(2rem);
  font-size: 1.6rem;
}
.zoom-enter-active,
.zoom-leave-active {
  animation-duration: 0.3s;
  animation-name: zoom;
}
.zoom-enter,
.zoom-leave-to {
  animation-name: zoom;
}
@keyframes zoom {
  from {
    opacity: 0;
    transform: scale3d(0.3, 0.3, 0.3);
  }
  100% {
    opacity: 1;
  }
}
@media only screen and (max-width: 1200px) {
  .poke-card {
      width: 45vw;
  }
 }
@media only screen and (max-width: 768px) {
  .poke-card {
      width: 80vw;
      margin-top: 2rem;
  }
  h2 {
  -webkit-text-stroke: .2rem #fff;
}
h3 {
  font-size: 1.8rem;
  padding: 2rem 4rem;
}
img {
  width: 15rem;
}
.poke-stats {
  gap: 1rem;
}
.poke-stat {
  text-transform: uppercase;
  font-size: 1.6rem;
  font-weight: 800;
  /* width: 40%; */
  list-style: none;
  width: 100%;
}
.poke-stat div {
  padding: .1rem;
  transform: translateZ(2rem);
  font-size: 1.6rem;
}
}
</style>