<template>
    <div class="card-list">
        <anime-card v-for="anime in animes" :id="anime.id" :key="anime.id"></anime-card>
    </div>
</template>
<script>
import AnimeCard from "./AnimeCard.vue";
import gql from "graphql-tag";

export default {
  components: {
    AnimeCard
  },
  data() {
    return {
      animes: []
    };
  },
  apollo: {
    animes: {
      query: gql`
        {
          animes {
            id
          }
        }
      `
    }
  }
};
</script>
<style scoped>
.card-list {
  display: flex;
}
</style>