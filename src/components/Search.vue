<template>
  <div class="main">
    <!-- add search icon -->
    <!-- bind input for search function and search on input change-->
    <input
      v-model="query"
      type="text"
      placeholder="Search artists"
      @input="search"
    />
    <h1>{{ query ? "Search Results" : "Browse Artists" }}</h1>
    <div v-if="query">
      <div v-if="query.length > 0 && searchResults === undefined">
        <h3>Sorry, no results were found for "{{ query }}".</h3>
      </div>
      <div v-else class="list">
        <div
          class="album"
          v-for="(item, index) in searchResults"
          :key="index"
          @mouseover="setActive(index)"
          @mouseout="setActive(false)"
        >
          <img class="artwork" :src="item.artwork_small" />
          <div class="info">
            <div>
              <h3>{{ item.artist }}</h3>
            </div>
            <div class="vote">
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
    <div v-else>
      <div class="list">
        <!-- set active class on mouseover for request btn -->
        <div
          class="album"
          v-for="(item, index) in browseResults"
          :key="index"
          @mouseover="setActive(index)"
          @mouseout="setActive(false)"
        >
          <img class="artwork" :src="item.artwork_small" />
          <div class="info">
            <div>
              <h3>{{ item.artist }}</h3>
            </div>
            <div class="vote">
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
  </div>
</template>

<script>
import { headers } from "../headers";

export default {
  name: "Search",
  data() {
    return {
      browseResults: [],
      query: "",
      searchResults: [],
      active: false,
      activeItem: null,
    };
  },
  methods: {
    search() {
      fetch(
        `https://api.rockbot.com/v3/engage/search_artists?query=${this.query}`,
        {
          headers,
        }
      )
        .then((res) => res.json())
        .then((data) => {
          this.searchResults = data.response;
        });
    },
    browseArtists() {
      // fetch and shuffle browse artist data
      fetch("https://api.rockbot.com/v3/engage/browse_artists", {
        headers,
      })
        .then((res) => res.json())
        .then((data) => {
          // shuffle full array
          for (let i = data.response.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [data.response[i], data.response[j]] = [
              data.response[j],
              data.response[i],
            ];
          }
          // display 25 results
          this.browseResults = data.response.slice(0, 25);
        });
    },
    setActive(index) {
      this.active = !this.active;
      this.activeItem = index;
    },
    request(artist_id) {
      fetch(
        `https://api.rockbot.com/v3/engage/request_artist?artist_id=${artist_id}`,
        {
          method: "POST",
          headers,
        }
      ).then((res) => res.json());
    },
  },
  mounted() {
    // render browse artists endpoint when there is no search input
    this.browseArtists();
  },
};
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

h1 {
  color: white;
}

.main {
  padding: 2.5em;
  justify-content: center;
  height: 650px;
  overflow: scroll;
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
</style>
