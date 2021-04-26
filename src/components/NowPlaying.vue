<template>
  <footer class="nowPlaying">
    <div class="album">
      <!-- <p>x</p> -->
    </div>
    <div class="info">
      <h4> Song </h4>
      <p> Artist</p>
    </div>
    <div class="vote">
      <div class="like"></div>
      <div class="like"></div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'NowPlaying',
  props: {
    msg: String
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
  background: gray;
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
  height: 50px;
  width: 50px;
  background: black;
  margin: 0 1em ;
}

h4 {
  margin: 1em 0 0 0;
}
</style>
