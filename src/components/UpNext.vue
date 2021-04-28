<template>
  <div class="main">
    <h1>Up Next</h1>
    <!-- map through queue data for song item -->
    <!-- feels like a syntaxical nightmare but its so easy wtf -->
    <div class="list">
      <div 
        class="album"
        v-for="(item, index) in upNext"
        :key="index">
        <img class="artwork" :src="item.artwork_large"/>
        <div class="info">
          <div>
            <h3>{{item.song}}</h3>
            <p>{{item.artist}}</p>
          </div>
          <div class="vote">
            <!-- add vote count on hover -->
            <!-- <button></button> -->
            <img src="../assets/icons/thumbs-down-regular.svg" class="like"/>
            <img src="../assets/icons/thumbs-up-regular.svg" class="like"/>
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
    upNext: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1 {
  color: white;
}

.main {
  padding: 2.5em;
  justify-content: center;
  /* height: 650px; */
  overflow: auto;
}

.list {
  display: flex;
  flex-wrap: wrap;
  line-height: .5;
}

.album {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: left;
  margin: 0 1em 1em 0;
  border-radius: 10px;
  height: 300px;
  min-width: 250px;
  background: #4e4e4e;
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
  height: 20px;
  width: 20px;
  /* background: black; */
  margin-left: 15px;
}

h3 {
  margin: 5px 0 10px 0;
}
p {
  margin: 0;
}

.artwork {
  height: 200px;
  width: 200px;
  align-self: center;
  object-fit: cover;
}
</style>
