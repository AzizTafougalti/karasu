<template>
    <div>
        <div v-if="$apollo.queries.anime.loading"><h1>Loading...</h1></div>
        <div v-else class="card">
            <img :src="anime.posterImage.small" alt="">
            <div class="details">
                <p>{{anime.title}}</p>
                <p>Episodes - {{anime.episodeCount}}</p>
            </div>
        </div>
    </div>
</template>
<script>
import gql from "graphql-tag";

export default {
  prop : {
    id : String
  },
  data() {
    return {
      id : '1',
      anime: {}
    };
  },
  apollo: {
    anime: {
      query: gql`
        query getAnime($id: ID) {
          anime(id: $id) {
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
          id: this.id
        };
      }
    }
  }
};
</script>
<style scoped>
.card {
  text-align: center;
  border-radius: 10px;
  display: inline-block;
  background-color: rgb(37, 37, 37);
  width: 284px;
}
.card>img {
  border-radius: 10px 10px 0 0;
}
.details {
  padding: 10px;
  color: rgb(211, 211, 211);
}
.details>p:first-child {
  font-size: larger;
}
button {
  border: none;
  outline: none;
  color: rgb(0, 136, 255);
  font-size: large;
  background-color: transparent;
}
button:hover {
  text-decoration: underline;
}
</style>