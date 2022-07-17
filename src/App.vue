<template>
  <input
    type="text"
    placeholder="Search"
    class="input"
    v-model="pokemonBusca"
  />

  <section class="container-cards">
    <div v-for="pokemon in pokemonsFiltrados" :key="pokemon.url">
      <PokemonComponent :name="pokemon.name" :url="pokemon.url" />
    </div>
  </section>
</template>

<script>
import PokemonComponent from "./components/pokemon.vue";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      pokemonsFiltrados: [],
      pokemonBusca: "",
    };
  },
  created: function () {
    fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
      .then((response) => response.json())
      .then((allpokemon) => {
        this.pokemonsFiltrados = allpokemon.results;
        this.pokemons = allpokemon.results;
      })
      .catch((error) => {
        throw Error("Promise failed", error);
      });
  },
  watch: {
    pokemonBusca(item) {
      let resultadoBusca = [];
      return this.pokemons.filter((pokemon) => {
        if (pokemon.name.includes(item.toLowerCase().trim())) {
          resultadoBusca.push(pokemon);
          this.pokemonsFiltrados = resultadoBusca;
        }
      });
    },
  },
  components: {
    PokemonComponent,
  },
};
</script>

<style>
html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}

body {
  background-color: #d3d3d345;
}

.container-cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 100%;
}

.input {
  outline: none;
  border: none;
  border-bottom: 1px solid #75777987;
  background-color: transparent;
  width: 97vw;
  margin: 15px 10px 9px 10px;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
