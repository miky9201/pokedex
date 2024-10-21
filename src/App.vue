<template>
  <Home />
  <!-- <PokemonDetails /> -->
</template>

<script lang="ts">
import { defineComponent } from "vue";
// import PokemonDetails from "./components/PokemonDetails.vue";
import Home from "./components/Home.vue";
// import axios, { AxiosResponse } from "axios";

export default defineComponent({
  components: {
    // PokemonDetails,
    Home,
  },
});
</script>

<style>
#app {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
