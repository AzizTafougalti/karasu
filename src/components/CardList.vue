<template>
<div class="uk-margin-medium-top">
  <h1 :id="about" class="uk-heading-divider">{{about}}</h1>
  <!-- <div v-if="$apollo.queries.animes.loading"><h1>Loading...</h1></div> -->
  <div id='trending'
  class="uk-child-width-1-2@s uk-child-width-1-4@m uk-child-width-1-6@l uk-child-width-1-8@xl uk-text-center"
  uk-grid>
      <anime-card v-for="anime in animes" :anime="anime" :key="anime.id"></anime-card>
  </div>
  <ul class="uk-pagination">
    <li><a @click="page--"><span class="uk-margin-small-right" uk-pagination-previous></span> Previous</a></li>
    <li class="uk-margin-auto-left"><a @click="page++">Next <span class="uk-margin-small-left" uk-pagination-next></span></a></li>
</ul>
</div>
</template>
<script>
import AnimeCard from "./AnimeCard.vue";
import gql from "graphql-tag";

export default {
  components: {
    AnimeCard
  },
  props: {
    about: String
  },
  data() {
    return {
      limit: 6,
      page: 130,
      animes: []
    };
  },
  apollo: {
    animes: {
      query: gql`
        query getAnime($limit: Int, $page: Int) {
          animes(limit: $limit, page: $page) {
            id
            title: canonicalTitle
            episodeCount
            posterImage {
              tiny
              small
              original
              large
            }
          }
        }
      `,
      variables() {
        return {
          page: this.page,
          limit: this.limit
        };
      }
    }
  }
};
</script>
<style scoped>
</style>