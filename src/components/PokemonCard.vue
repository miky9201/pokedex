<template>
  <div class="list-item" @click="handleClick(pokemonId)">
    <div class="list-item-number">
      <p v-if="pokemonId < 10" class="details-number">#00{{ pokemonId }}</p>
      <p v-else-if="pokemonId < 100 && pokemonId >= 10" class="details-number">
        #0{{ pokemonId }}
      </p>
      <p v-else class="details-number">#{{ pokemonId }}</p>
    </div>
    <img class="list-item-img" :src="pokemonImg" alt="" />

    <div class="list-item-name">
      <p>{{ pokemonName }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    pokemonId: {
      type: Number,
      default: 0,
    },
    pokemonName: String,
    pokemonImg: String,
  },
  methods: {
    handleClick(id: number) {
      this.$emit("card-clicked");
      this.$emit("selected-card-id", id);
    },
  },
});
</script>

<style>
.list-item {
  display: flex;
  width: 6.5rem;
  height: 6.75rem;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  border-radius: 0.5rem;
  background: var(--Grayscale-White, #fff);
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.2);
}

.list-item-number {
  display: flex;
  padding: 0.25rem 0.5rem 0rem 0.5rem;
  justify-content: flex-end;
  align-items: flex-start;
  gap: 0.5rem;
  align-self: stretch;
}

.list-item-number p {
  color: var(--Grayscale-Medium, #666);
  text-align: right;

  /* Body/Caption */
  font-family: Poppins;
  font-size: 0.5rem;
  font-style: normal;
  font-weight: 400;
  line-height: 0.75rem; /* 150% */
}

.list-item-img {
  z-index: 1;
  width: 4.5rem;
  height: 4.5rem;
  margin-bottom: -1.5rem;
}

.list-item-name {
  display: flex;
  padding: 1.5rem 0.5rem 0.25rem 0.5rem;
  align-items: flex-start;
  align-self: stretch;
  border-radius: 0.4375rem;
  background: var(--Grayscale-Background, #efefef);
}

.list-item-name p {
  text-transform: capitalize;
  flex: 1 0 0;
  color: var(--Grayscale-Dark, #1d1d1d);
  text-align: center;
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 1rem;
}
</style>
