<template>
  <div class="main">
    <h1>Trending Now</h1>
    <div class="list">
      <div
        class="album"
        v-for="(item, index) in topArtists"
        :key="index"
        @mouseover="setActive(index)"
        @mouseout="setActive(false)"
      >
        <img class="artwork" :src="item.artwork_large" />
        <div class="info">
          <div>
            <h3>{{ item.artist }}</h3>
          </div>
          <div class="vote">
            <!-- add vote count on hover -->
            <img
              v-show="activeItem === index"
              src="../assets/icons/plus-solid.svg"
              class="add"
              v-on:click="request(item.artist_id)"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { headers } from "../headers";

export default {
  name: "Trending",
  data() {
    return {
      active: false,
      activeItem: null,
    };
  },
  props: {
    topArtists: Array,
  },
  methods: {
    setActive(index) {
      this.active = !this.active;
      this.activeItem = index;
    },
    request(artist_id) {
      // reusing search function until I figure out how to use $emit
      fetch(
        `https://api.rockbot.com/v3/engage/request_artist?artist_id=${artist_id}`,
        {
          method: "POST",
          headers,
        }
      ).then((res) => res.json());
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: white;
}

.main {
  padding: 2.5em;
  justify-content: center;
  height: 650px;
  overflow: auto;
}

.list {
  display: flex;
  flex-wrap: wrap;
  line-height: 0.5;
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

.add {
  height: 30px;
  width: 30px;
  margin-top: -235px;
  margin-right: -15px;
  background: #56d092;
  border: 3px solid #56d092;
  border-radius: 100%;
  background: "../assets/icons/plus-solid.svg";
}

.add:hover {
  cursor: pointer;
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

::-webkit-scrollbar {
  -webkit-appearance: none;
  width: 7px;
}

::-webkit-scrollbar-thumb {
  border-radius: 4px;
  background-color: rgba(36, 36, 36, 0.5);
  box-shadow: 0 0 1px rgba(255, 255, 255, 0.5);
}
</style>
