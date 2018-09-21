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
    <li class="uk-margin-auto-left"><a @click="showMore">Next <span class="uk-margin-small-left" uk-pagination-next></span></a></li>
</ul>
</div>
</template>
<script>
import AnimeCard from "./AnimeCard.vue";
import gql from "graphql-tag";
import { json } from "body-parser";
const LIMIT = 6;

export default {
  components: {
    AnimeCard
  },
  props: {
    about: String
  },
  data() {
    return {
      page: 1
    };
  },
  apollo: {
    animes: {
      query: gql`
        query animes($limit: Int, $page: Int) {
          animes(limit: $limit, page: $page) {
            id
            title: canonicalTitle
            episodeCount
            posterImage {
              small
            }
          }
        }
      `,
      variables: {
        page: 1,
        limit: LIMIT
      }
    }
  },
  methods: {
    showMore() {
      this.page++;
      this.$apollo.queries.animes.fetchMore({
        variables: {
          page: this.page,
          limit: LIMIT
        },
        updateQuery: (previousResult, { fetchMoreResult }) => {
          const newAnimes = fetchMoreResult.animes;

          return {
            animes: [...previousResult.animes, ...newAnimes]
          };
        }
      });
    }
  }
};
</script>
<style scoped>
</style>