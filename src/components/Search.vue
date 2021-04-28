<template>
  <div class="main">
    <!-- add search icon -->
    <!-- bind input for search function and search on input change-->
   <input v-model="query" type="text" placeholder="Search artists" @input="search">
  </div>
</template>

<script>
import { headers } from '../headers';

  export default {
    name: 'Search',
    data() {
      return {
        query: "",
        results: []
      }
    },
    props: {
     
    },
    methods: {
      search() {
      console.log(this.query)
      fetch(`https://api.rockbot.com/v3/engage/search_artists?query=${this.query}`, {
        headers
      })
      .then((res) => res.json())
      .then((data) => {
        this.results = data.response
        console.log(data.response)
      })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

input {
  height: 2.5em;
  width: 18em;
  padding-left: 10px;
  border: none;
  border-radius: 10px;
  font-size: 16px;
}
input:focus {
  outline: none;
}
.main {
  margin-left: 5%;
}

</style>
