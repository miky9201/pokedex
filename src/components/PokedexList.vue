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
      <p :key="pokemon.name" v-for="pokemon in resultQuery">
        <PokemonCard
          :pokemonId="pokemon.id"
          :pokemonName="pokemon.name"
          :pokemonImg="pokemon.img"
          @card-clicked="$emit('card-clicked')"
          @selected-card-id="$emit('selected-card-id')"
        />
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import PokemonCard from "./PokemonCard.vue";

interface PokedexList {
  id: number;
  name: string;
  img: string;
}

interface Data {
  searchContent: string;
  pokedexList: PokedexList[];
}

export default defineComponent({
  props: {
    isCardClicked: Boolean,
  },
  components: {
    PokemonCard,
  },
  data(): Data {
    return {
      searchContent: "",
      pokedexList: [],
    };
  },
  computed: {
    resultQuery(): PokedexList[] {
      if (this.searchContent) {
        return this.pokedexList.filter((pokemon) => {
          return this.searchContent
            .toLowerCase()
            .split(" ")
            .every((v) => pokemon.name.toLowerCase().includes(v));
        });
      } else {
        return this.pokedexList;
      }
    },
  },
  methods: {
    getPokedexList() {
      fetch(`https://pokeapi.co/api/v2/pokemon/?limit=151&offset=0`)
        .then((response) => response.json())
        .then((list) => {
          const fetchPromises = list.results.map((result: { url: string }) =>
            fetch(result.url)
              .then((res) => res.json())
              .then((el) => ({
                id: el.id,
                name: el.name,
                img: el.sprites.other["official-artwork"].front_default,
              }))
          );

          return Promise.all(fetchPromises);
        })
        .then((pokemonArray) => {
          this.pokedexList = pokemonArray; // Maintenant dans le bon ordre
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
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  /* grid-auto-rows: minmax(100px, auto); */
  padding: 1.5rem 0.75rem 1.5rem 0.75rem;

  /* gap: 0.5rem; */
  align-self: stretch;
  border-radius: 0.5rem;
  background: var(--Grayscale-White, #fff);

  /* Inner Shadow/2 dp */
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.25) inset;
  overflow: overlay;
}

.pokedex-list::-webkit-scrollbar {
  display: none;
}
</style>
