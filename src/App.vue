<template>
  <PokedexList v-if="!isDetailDisplayed" @get-pokemon-id="getPokemonId" />
  <PokemonDetails
    v-if="isDetailDisplayed"
    :id="cardSelected"
    @handle-click-back="handleClickBack"
    @handle-previous-pokemon="handlePreviousPokemon"
    @handle-next-pokemon="handleNextPokemon"
  />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import PokemonDetails from "./components/PokemonDetails.vue";
import PokedexList from "./components/PokedexList.vue";

export default defineComponent({
  components: {
    PokemonDetails,
    PokedexList,
  },
  data() {
    return {
      isDetailDisplayed: false,
      cardSelected: 0,
    };
  },
  methods: {
    getPokemonId(id: number) {
      this.cardSelected = id;
      this.isDetailDisplayed = true;
    },
    handleClickBack() {
      this.isDetailDisplayed = false;
    },
    handlePreviousPokemon() {
      this.cardSelected--;
    },
    handleNextPokemon() {
      this.cardSelected++;
    },
  },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

#app {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
