<template>
  <div class="main">
    <!-- <font-awesome-icon icon="fas fa-search" /> -->
   <input type="text" placeholder="Search artists" onchange={}>
  </div>
</template>

<script>
// import { library } from '@fortawesome/fontawesome-svg-core';
// import { faSearch } from '@fortawesome/free-solid-svg-icons';

// SEARCH ON CHANGE
  export default {
    name: 'Search',
    props: {
      msg: String
    },
    methods: {

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

input {
  height: 2.5em;
  width: 15em;
  padding-left: 10px;
  border: 1px solid black;
  border-radius: 10px;
  font-size: 16px;
}
input:focus {
  outline: none;
}
.main {
  margin-left: 65%;
}

</style>
