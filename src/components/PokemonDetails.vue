<template>
  <div :class="`${pokemon.color} details-container`">
    <img class="pokeball" src="../assets/pokeball.svg" alt="" />

    <div class="details-header">
      <img
        class="details-icon-arrowback"
        src="../assets/arrow_back.svg"
        alt="arrow-back"
        @click="$emit('handle-click-back')"
      />
      <h1 class="details-title">{{ pokemon.name }}</h1>
      <h2 v-if="pokemon.id < 10" class="details-number">#00{{ pokemon.id }}</h2>
      <h2
        v-else-if="pokemon.id < 100 && pokemon.id >= 10"
        class="details-number"
      >
        #0{{ pokemon.id }}
      </h2>
      <h2 v-else class="details-number">#{{ pokemon.id }}</h2>
    </div>
    <div class="details-pokemon-img">
      <img
        class="details-icon-chevronleft"
        src="../assets/chevron_left.svg"
        alt="chevron-left"
        @click="$emit('handle-previous-pokemon')"
      />
      <img class="silhouette" :src="pokemon.image" alt="" />
      <img
        class="details-icon-chevronright"
        src="../assets/chevron_right.svg"
        alt="chevron-right"
        @click="$emit('handle-next-pokemon')"
      />
    </div>
    <div class="details-card">
      <div class="details-type-container">
        <div
          :key="pokemonType.type.name"
          v-for="pokemonType in pokemon.pokemonTypes"
          :class="`${pokemonType.type.name} details-type`"
        >
          {{ pokemonType.type.name }}
        </div>
      </div>
      <h2 :class="`${pokemon.color}-text details-subtitle`">About</h2>
      <div class="details-attribute">
        <div class="details-frame">
          <div class="details-subframe">
            <img src="../assets/weight.svg" alt="" />
            <p>{{ pokemon.weight / 10 }} kg</p>
          </div>
          <div class="details-info-label">Weight</div>
        </div>
        <div class="hr"></div>
        <div class="details-frame">
          <div class="details-subframe">
            <img src="../assets/straighten.svg" alt="" />
            <p>{{ pokemon.height / 10 }} m</p>
          </div>
          <div class="details-info-label">Height</div>
        </div>
        <div class="hr"></div>
        <div class="details-frame">
          <p
            :key="pokemonAbility.ability.name"
            v-for="pokemonAbility in pokemon.pokemonAbilities"
          >
            {{ pokemonAbility.ability.name }}
          </p>

          <div class="details-info-label">Abilities</div>
        </div>
      </div>
      <div class="description">
        {{ pokemon.description }}
      </div>
      <h2 :class="`${pokemon.color}-text details-subtitle`">Base Stats</h2>
      <div class="details-base-stats">
        <div class="details-label-container">
          <div :class="`${pokemon.color}-text details-label`">HP</div>
          <div :class="`${pokemon.color}-text details-label`">ATK</div>
          <div :class="`${pokemon.color}-text details-label`">DEF</div>
          <div :class="`${pokemon.color}-text details-label`">SATK</div>
          <div :class="`${pokemon.color}-text details-label`">SDEF</div>
          <div :class="`${pokemon.color}-text details-label`">SPD</div>
        </div>
        <div class="hr"></div>
        <div class="details-data-container">
          <div
            :key="stat.base_stat"
            v-for="stat in pokemon.pokemonStats"
            class="details-data"
          >
            {{ stat.base_stat }}
          </div>
        </div>
        <div class="details-chart-container">
          <div
            :key="stat.base_stat"
            v-for="stat in pokemon.pokemonStats"
            class="details-chart"
          >
            <div class="details-chart-value">
              <div
                :style="{ width: stat.base_stat / 2 + '%' }"
                :class="`${pokemon.color} details-chart-value-number`"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

interface PokemonType {
  type: {
    name: string;
  };
}

interface PokemonAbility {
  ability: {
    name: string;
  };
}

interface PokemonStat {
  name: string;
  base_stat: number;
}

interface Pokemon {
  name: string;
  id: number;
  image: string;
  pokemonTypes: PokemonType[];
  height: number;
  weight: number;
  pokemonAbilities: PokemonAbility[];
  pokemonStats: PokemonStat[];
  color: string;
  description: string;
}

interface Data {
  pokemon: Pokemon;
}

export default defineComponent({
  props: {
    id: Number,
  },
  data(): Data {
    return {
      pokemon: {
        name: "",
        id: 0,
        image: "",
        pokemonTypes: [],
        height: 0,
        weight: 0,
        pokemonAbilities: [],
        pokemonStats: [],
        color: "",
        description: "",
      },
    };
  },
  watch: {
    id() {
      this.getPokemonInfo();
      this.getPokemonColor();
    },
  },
  methods: {
    getPokemonInfo() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.$props.id}`)
        .then((response) => {
          response.json().then((pokemon) => {
            this.pokemon.name = pokemon.name;
            this.pokemon.id = pokemon.id;
            this.pokemon.image =
              pokemon.sprites.other["official-artwork"].front_default;
            this.pokemon.pokemonTypes = pokemon.types;
            this.pokemon.height = pokemon.height;
            this.pokemon.weight = pokemon.weight;
            this.pokemon.pokemonAbilities = pokemon.abilities;
            this.pokemon.pokemonStats = pokemon.stats;
            this.pokemon.color = pokemon.types[0].type.name;
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
    getPokemonColor() {
      fetch(`https://pokeapi.co/api/v2/pokemon-species/${this.$props.id}`)
        .then((response) => {
          response.json().then((result) => {
            this.pokemon.description =
              result.flavor_text_entries[0].flavor_text;
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
  mounted() {
    this.getPokemonInfo();
    this.getPokemonColor();
  },
});
</script>

<style>
.hr {
  border: none;
  border-left: 1px solid #e0e0e0;
  height: 100%;
  width: 0.0625rem;
  align-self: stretch;
}

.details-container {
  display: flex;
  width: 22.5rem;
  height: 40rem;
  padding: 0.25rem;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
  background: var(--Identity-Primary, #858585);
}

.pokeball {
  width: 208px;
  height: 208px;
  position: absolute;
  margin: 0.5rem 0.5rem 26.5rem 9rem;
}

.details-icon-arrowback {
  width: 2rem;
  height: 2rem;
}

.details-header {
  width: 19.5rem;
  height: 2rem;
  display: flex;
  padding: 1.25rem 1.25rem 1.5rem 1.25rem;
  align-items: center;
  gap: 0.5rem;
  align-self: stretch;
}

.details-title {
  color: var(--Grayscale-White, #fff);
  /* Header/Headline */
  font-family: Poppins;
  font-size: 1.5rem;
  font-style: normal;
  font-weight: 700;
  text-transform: capitalize;
  line-height: 2rem; /* 133.333% */
  flex: 1 0 0;
}

.details-number {
  color: var(--Grayscale-White, #fff);

  /* Header/Subtitle 2 */
  font-family: Poppins;
  font-size: 0.75rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 133.333% */
}

.details-pokemon-img {
  height: 7rem;
  width: 19.5rem;
  display: flex;
  padding: 1rem 1.25rem;
  margin: 0 0.25rem;
  justify-content: space-between;
  align-items: flex-end;
  flex: 1 0 0;
  align-self: stretch;
}

.details-icon-chevronleft,
.details-icon-chevronright {
  z-index: 1;
  width: 1.5rem;
  height: 1.5rem;
}

.silhouette {
  z-index: 0;
  margin: 0 auto -4.4rem auto;
  display: flex;
  width: 12.5rem;
  height: 12.5rem;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
}

.details-card {
  display: flex;
  height: 21rem;
  height: 21rem;
  padding: 3.5rem 1.25rem 1.25rem 1.25rem;
  flex-direction: column;
  align-items: flex-start;
  gap: 1rem;
  flex-shrink: 0;
  align-self: stretch;
  border-radius: 0.5rem;
  background: var(--Grayscale-White, #fff);
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.25) inset;
}

.details-type-container {
  height: 1.25rem;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 1rem;
  align-self: stretch;
}

.details-type {
  height: 1rem;
  display: flex;
  padding: 0.125rem 0.5rem;
  flex-direction: column;
  align-items: flex-start;
  border-radius: 0.625rem;
  background: var(--Grayscale-Medium, #666);
  color: var(--Grayscale-White, #fff);
  /* Header/Subtitle 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 160% */
  text-transform: capitalize;
}

.details-subtitle {
  align-self: stretch;
  color: var(--Grayscale-Wireframe, #b8b8b8);
  text-align: center;
  /* Header/Subtitle 1 */
  font-family: Poppins;
  font-size: 0.875rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 114.286% */
}

.details-attribute {
  height: 3rem;
  display: flex;
  align-items: flex-start;
  align-self: stretch;
  background: var(--Grayscale-White, #fff);
}

.details-frame {
  height: 3rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  gap: 0.25rem;
  flex: 1 0 0;
}

.details-subframe {
  height: 1rem;
  display: flex;
  padding: 0.5rem 0rem;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  align-self: stretch;
}

.details-frame p {
  color: var(--Grayscale-Dark, #1d1d1d);
  text-align: justify;

  /* Body/Body 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 0.8rem; /* 160% */
  text-transform: capitalize;
}

.details-info-label {
  align-self: stretch;
  color: var(--Grayscale-Medium, #666);
  text-align: center;

  /* Body/Caption */
  font-family: Poppins;
  font-size: 0.5rem;
  font-style: normal;
  font-weight: 400;
  line-height: 0.75rem; /* 150% */
}

.description {
  height: 3.75rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  flex: 1 0 0;
  align-self: stretch;
  color: var(--Grayscale-Dark, #1d1d1d);
  text-align: justify;

  /* Body/Body 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 1rem; /* 160% */
}

.details-base-stats {
  height: 6rem;
  display: flex;
  align-items: flex-start;
  gap: 0.5rem;
  align-self: stretch;
  background: var(--Grayscale-White, #fff);
}

.details-label-container {
  width: 1.69rem;
  height: 6rem;
  display: flex;
  padding-right: 0.25rem;
  flex-direction: column;
  align-items: flex-start;
}

.details-label {
  width: 1.6875rem;
  color: var(--Grayscale-Wireframe, #b8b8b8);
  text-align: right;

  /* Header/Subtitle 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 160% */
}

.details-data-container {
  width: 1.19rem;
  height: 6rem;
  display: flex;
  padding-left: 0.25rem;
  flex-direction: column;
  align-items: flex-start;
}

.details-data {
  width: 1.1875rem;
  color: var(--Grayscale-Dark, #1d1d1d);

  /* Body/Body 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 1rem; /* 160% */
}

.details-chart-container {
  width: 14.6rem;
  height: 6rem;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  flex: 1 0 0;
}

.details-chart {
  width: 14.6rem;
  height: 1rem;
  display: flex;
  height: 1rem;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  gap: -0.25rem;
  align-self: stretch;
}

.details-chart-value {
  width: 14.6rem;
  height: 0.25rem;
  display: flex;
  align-items: flex-start;
  align-self: stretch;
  /* opacity: 0.2; */
  background: var(--Grayscale-Wireframe, #f0f0f0);
  border-radius: 0.25rem;
}

.details-chart-value-number {
  width: 60%;
  height: 0.25rem;

  background: var(--Grayscale-Wireframe, #8b8b8b);
  border-radius: 0.25rem;
}

.bug {
  background-color: #a7b723;
}

.dark {
  background-color: #75574c;
}

.dragon {
  background-color: #7037ff;
}

.electric {
  background-color: #f9cf30;
}

.fairy {
  background-color: #e69eac;
}

.fighting {
  background-color: #c12239;
}

.fire {
  background-color: #f57d31;
}

.flying {
  background-color: #a891ec;
}

.ghost {
  background-color: #70559b;
}

.normal {
  background-color: #aaa67f;
}

.grass {
  background-color: #74cb48;
}

.ground {
  background-color: #dec16b;
}

.ice {
  background-color: #9ad6df;
}

.poison {
  background-color: #a43e9e;
}

.psychic {
  background-color: #fb5584;
}

.rock {
  background-color: #b69e31;
}

.steel {
  background-color: #b7b9d0;
}

.water {
  background-color: #6493eb;
}

.bug-text {
  color: #a7b723;
}

.dark-text {
  color: #75574c;
}

.dragon-text {
  color: #7037ff;
}

.electric-text {
  color: #f9cf30;
}

.fairy-text {
  color: #e69eac;
}

.fighting-text {
  color: #c12239;
}

.fire-text {
  color: #f57d31;
}

.flying-text {
  color: #a891ec;
}

.ghost-text {
  color: #70559b;
}

.normal-text {
  color: #aaa67f;
}

.grass-text {
  color: #74cb48;
}

.ground-text {
  color: #dec16b;
}

.ice-text {
  color: #9ad6df;
}

.poison-text {
  color: #a43e9e;
}

.psychic-text {
  color: #fb5584;
}

.rock-text {
  color: #b69e31;
}

.steel-text {
  color: #b7b9d0;
}

.water-text {
  color: #6493eb;
}

/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)  
*/

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
  height: 100vh;
}
/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}
body {
  line-height: 1;
}
ol,
ul {
  list-style: none;
}
blockquote,
q {
  quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
</style>
