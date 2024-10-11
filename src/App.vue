<template>
  <PokemonDetails />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import PokemonDetails from "./components/PokemonDetails.vue";
// import axios, { AxiosResponse } from "axios";

export default defineComponent({
  components: {
    PokemonDetails,
  },
});
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
