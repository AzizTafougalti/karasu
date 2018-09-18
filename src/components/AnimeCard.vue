<template>
  <div>
    <div class="uk-card uk-card-small uk-align-center uk-card-hover uk-card-default my-card" uk-scrollspy="cls: uk-animation-slide-left; repeat: true">
      <div class="uk-card-media-top">
          <img :src="anime.posterImage.small" :alt="anime.title">
      </div>
      <div class="uk-card-body">
        <p>{{anime.title}}</p>
        <p>Episodes - {{anime.episodeCount}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    anime: Object
  }
};
</script>

<style scoped>
.my-card{
  max-width: 284px;
  border-radius: 10px;
}
.uk-card-media-top>img{
  border-radius: 10px 10px 0 0;
}
</style>