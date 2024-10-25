<template>
  <div class="list-item">
    <div class="list-item-number">
      <p>054</p>
    </div>
    {{ pokemonName }}
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    pokemonName: String,
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
</style>
