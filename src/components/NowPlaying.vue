<template>
  <footer class="nowPlaying">
    <img class="album" :src="nowPlaying.artwork_small">
    <div class="info">
      <h4> {{nowPlaying.song}} </h4>
      <p> {{nowPlaying.artist}}</p>
    </div>
    <div class="vote">
      <button class="like"><img class="thumb-down" src="../assets/icons/thumbs-down-regular.svg" /></button>
      <button class="like"><img class="thumb-up" src="../assets/icons/thumbs-up-regular.svg" /></button>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'NowPlaying',
  props: {
    nowPlaying: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.nowPlaying {
  display: flex;
  align-items: center;
  margin-left: -12em;
  width: 125%;
  height: 6em;
  background: #4e4e4e;
  color: white;
  padding: 1em 1em 1em 2em;
}

.album {
  height: 70px;
  width: 70px;
  background: black;
}

.info {
  margin-left: 1em;
  font-size: 16px;
  line-height: .5;
}

.vote {
  display: flex;
  margin-left: 35%;
}

.like {
  height: 75px;
  width: 75px;
  /* background: tomato; */
  margin: 0 1em ;
  border: 5px solid lightgrey;
  border-radius: 100%;
}

.thumb-down {
  height: 40px;
  margin: 5px 0 0 5px;
  /* background: tomato; */
}

.thumb-up {
  height: 40px;
  margin: 0px 0 0 5px;
  /* background:palegreen; */
}

h4 {
  margin: 1em 0 0 0;
}
</style>
