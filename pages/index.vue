<template>
  <div>
    <h1>{{ title }}</h1>
    <button @click="clickMe">click me</button>

    <p v-if="pending">Loading...</p>
    <template v-else>
      <ul>
        <li v-for="pokemon in pokemons" :key="pokemon.id">
          <NuxtLink :to="`/pokemon/${pokemon.id}`">
            {{ pokemon.name.english }}
          </NuxtLink>
        </li>
      </ul>
    </template>
  </div>
</template>

<script setup>
const { data: pokemons, pending } = await useAsyncData(
  "pokemons",
  () => $fetch("/api/pokemon"),
  { lazy: true }
);

const title = ref("Pokemon list");

const clickMe = () => {
  title.value = "I CHANGED MY TITLE YESSS";
};
</script>
