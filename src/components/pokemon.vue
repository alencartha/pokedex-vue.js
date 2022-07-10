<template>
  <div class="card-pokemon">
    <img :src="imgPokemon" class="img-pokemon" />
    <div class="label-pokemon">
      <p>{{ name }}</p>
      <p>#{{ idPokemon }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonComponent",
  data() {
    return {
      imgPokemon: "",
      idPokemon: "",
    };
  },
  props: {
    name: String,
    url: String,
  },
  created: function () {
    fetch(this.url)
      .then((response) => response.json())
      .then((pokemonData) => {
        this.idPokemon = pokemonData.order;
        this.imgPokemon = pokemonData.sprites.back_default;
      })
      .catch((error) => {
        throw Error("Promise failed", error);
      });
  },
};
</script>


<style>
.card-pokemon {
  font-family: Arial, Helvetica, sans-serif;
  color: #3e4041;
  text-transform: capitalize;
  font-size: 14px;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  width: 180px;
  height: 110px;
  background-color: #fff;
  margin: 5px;
  border-radius: 2px;
  -webkit-box-shadow: -1px 0px 6px 1px rgba(0, 0, 0, 0.105);
  -moz-box-shadow: -1px 0px 6px 1px rgba(0, 0, 0, 0.105);
  box-shadow: -1px 0px 6px 1px rgba(0, 0, 0, 0.105);
}

.img-pokemon {
  width: 80px;
  height: 80px;
}

.label-pokemon {
  display: flex;
  justify-content: space-between;
  width: 90%;
}
</style>
