<template>
  <div class="pokedex-list-container">
    <div class="pokedex-list-header">
      <div class="pokedex-list-header-title">
        <img src="../assets/pokeball-small.svg" />
        <h1>Pokédex</h1>
      </div>
      <div class="pokedex-list-header-filters">
        <div class="pokedex-list-header-filters-search">
          <img src="../assets/search.svg" />
          <input
            class="pokedex-list-header-filters-text"
            placeholder="Search"
            type="search"
            v-model="searchContent"
          />
        </div>
        <div class="pokedex-list-header-filters-sort">
          <img src="../assets/sort.svg" />
        </div>
      </div>
    </div>
    <div class="pokedex-list">
      <p :key="pokemon.name" v-for="pokemon in pokedexList">
        {{ pokemon.name }}
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

interface PokedexList {
  name: string;
}

interface Data {
  searchContent: string;
  pokedexList: PokedexList[];
}

export default defineComponent({
  data(): Data {
    return {
      searchContent: "",
      pokedexList: [],
    };
  },
  watch: {
    searchContent(newSearchContent) {
      console.log(newSearchContent);
    },
  },
  methods: {
    getPokedexList() {
      fetch(`https://pokeapi.co/api/v2/pokemon/?limit=150&offset=0`)
        .then((response) => {
          response.json().then((list) => {
            console.log(list.results);
            this.pokedexList = list.results;
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
  mounted() {
    this.getPokedexList();
  },
});
</script>

<style>
.pokedex-list-container {
  display: flex;
  width: 22.5rem;
  height: 40rem;
  padding: 0.25rem;
  flex-direction: column;
  align-items: flex-start;
  flex-shrink: 0;
  background: var(--Identity-Primary, #dc0a2d);
}

.pokedex-list-header {
  display: flex;
  padding: 0.75rem 0.75rem 1.5rem 0.75rem;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.5rem;
  align-self: stretch;
}

.pokedex-list-header-title {
  display: flex;
  align-items: center;
  gap: 1rem;
  align-self: stretch;
}

.pokedex-list-header-title img {
  width: 1.5rem;
  height: 1.5rem;
}
.pokedex-list-header-title h1 {
  color: var(--Grayscale-White, #fff);

  /* Header/Headline */
  font-family: Poppins;
  font-size: 1.5rem;
  font-style: normal;
  font-weight: 700;
  line-height: 2rem; /* 133.333% */
}

.pokedex-list-header-filters {
  display: flex;
  align-items: center;
  gap: 1rem;
  align-self: stretch;
}
.pokedex-list-header-filters-search {
  display: flex;
  padding: 0.5rem 1rem 0.5rem 0.75rem;
  align-items: center;
  gap: 0.5rem;
  flex: 1 0 0;
  border-radius: 1rem;
  background: var(--Grayscale-White, #fff);

  /* Inner Shadow/2 dp */
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.25) inset;
}

.pokedex-list-header-filters-text {
  flex: 1 0 0;
  color: var(--Grayscale-Medium, #666);
  /* Body/Body 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 1rem; /* 160% */
  border: none;
}

.pokedex-list-header-filters-sort {
  display: flex;
  padding: 0.5rem;
  align-items: flex-start;
  gap: 0.5rem;
  border-radius: 1rem;
  background: var(--Grayscale-White, #fff);

  /* Inner Shadow/2 dp */
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.25) inset;
}

.pokedex-list {
  display: flex;
  padding: 1.5rem 0.75rem 0rem 0.75rem;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.5rem;
  flex: 1 0 0;
  align-self: stretch;
  border-radius: 0.5rem;
  background: var(--Grayscale-White, #fff);
  overflow: hidden;

  /* Inner Shadow/2 dp */
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.25) inset;
}
</style>
