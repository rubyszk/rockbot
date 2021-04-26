<template>
  <div class="main">
    <h1>Up Next</h1>
    <div class="list">
      <div class="album">
        <div class="item"/>
        <div class="info">
          <div>
            <h3>Song</h3>
            <p>Artist</p>
          </div>
          <div class="vote">
            <div class="like"/>
            <div class="like"/>
          </div>
        </div>
      </div>
      <div class="album">
        <div class="item"/>
        <div class="info">
          <div>
            <h3>Song</h3>
            <p>Artist</p>
          </div>
          <div class="vote">
            <div class="like"/>
            <div class="like"/>
          </div>
        </div>
      </div>
      <div class="album">
        <div class="item"/>
        <div class="info">
          <div>
            <h3>Song</h3>
            <p>Artist</p>
          </div>
          <div class="vote">
            <div class="like"/>
            <div class="like"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UpNext',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.main {
  /* text-align: center; */
  /* display: flex; */
  padding: 2.5em;
  justify-content: center;
  flex-direction: column;
  /* overflow: auto; */
}

.list {
  display: flex;
  justify-content: center;
  line-height: .5;
  /* text-align: left; */
}

.album {
  display: flex;
  flex-direction: column;
  justify-content: center;
  /* align-items: center; */
  text-align: left;
  margin: 0 3em 3em 0;
  border-radius: 10px;
  height: 300px;
  min-width: 250px;
  background: gray;
  color: white;
}

.info {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  padding: 10px 25px 0 25px;
}

.vote {
  display: flex;
}

.like {
  height: 25px;
  width: 25px;
  background: black;
  margin-left: 10px;
}

h3 {
  margin: 5px 0 10px 0;
}
p {
  margin: 0;
}

.item {
  height: 200px;
  width: 200px;
  align-self: center;
  background: black;
}
</style>
