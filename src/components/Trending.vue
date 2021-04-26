<template>
  <div class="main">
    <h1>Up Next</h1>
    <div class="albums">
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Trending',
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
  justify-content: center;
  flex-direction: column;
}

</style>
