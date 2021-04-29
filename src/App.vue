<template>
  <div id="app">
    <div class="sidebar">
      <!-- nav highlight active state -->
      <ul>
        <li :class="currentView === 'Home' ? 'active' : null">
          <a @click="changeView('Home')">
            <img class="sidebar-icon" src="./assets/icons/home-solid.svg" />
            Home
          </a>
        </li>
        <li :class="currentView === 'Search' ? 'active' : null">
          <a @click="changeView('Search')">
            <img class="sidebar-icon" src="./assets/icons/search-solid.svg"/> 
            Search
          </a>
        </li>
        <li :class="currentView === 'Trending' ? 'active' : null">
          <a @click="changeView('Trending')">
            <img class="sidebar-icon" src="./assets/icons/fire-alt-solid.svg" />
            What's Hot
          </a>
        </li>
      </ul>
    </div>
    <div class="content">
      <Search v-show="currentView === 'Search'" />
      <div class="header">
        <img class="user-icon" src="./assets/icons/robot-solid.svg" />
        <h5>Rockbot HQ</h5>
      </div>
      <UpNext v-show="currentView === 'Home'" :upNext="upNext" />
      <Trending v-show="currentView === 'Trending'" :topArtists="topArtists" />
      <NowPlaying :nowPlaying="nowPlaying" />
    </div>
  </div>
</template>

<script>
import { headers } from "./headers";
import NowPlaying from "./components/NowPlaying";
import UpNext from "./components/UpNext";
import Search from "./components/Search";
import Trending from "./components/Trending";

export default {
  name: "App",

  components: {
    NowPlaying,
    UpNext,
    Search,
    Trending,
  },
  data() {
    return {
      currentView: "Home",
      views: ["Home", "Search", "Trending"],
      nowPlaying: {},
      upNext: [],
      browseArtists: {},
      topArtists: [],
      searchResults: {},
    };
  },
  computed: {
    window: () => window,
    isPlaying() {
      return `${this.nowPlaying}`;
    },
  },
  methods: {
    changeView(view) {
      this.currentView = view;
    },
    fetchNowPlaying() {
      // API call fetches now playing and queue data
      fetch("https://api.rockbot.com/v3/engage/now_playing?queue=1", {
        headers,
      })
        .then((res) => res.json())
        .then((data) => {
          this.nowPlaying = data.response.now_playing;
          this.upNext = data.response.queue;
        });
      // fetch every 30 seconds
      window.setInterval(() => {
        this.fetchNowPlaying()
      }, 30000)
    },
    fetchTopArtists() {
      fetch("https://api.rockbot.com/v3/engage/top_artists", {
        headers,
      })
        .then((res) => res.json())
        .then((data) => {
          this.topArtists = data.response;
        });
    },
  },
  mounted() {
    // call on mount (useEffect?)
    this.fetchNowPlaying();
    this.fetchTopArtists();
  },
};
</script>

<style>
body {
  margin: 0px;
  height: 100%;
  display: flex;
}

#app {
  display: flex;
  height: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
  background: rgb(209, 225, 230);
  background: linear-gradient(
    4deg,
    rgba(33, 33, 33, 1) 34%,
    rgba(96, 96, 96, 1) 73%,
    rgba(154, 154, 154, 1) 97%
  );
}

.header {
  display: flex;
  justify-content: space-between;
  width: 130px;
  right: 3em;
  position: absolute;
  background: #4e4e4e;
  border-radius: 10px;
  height: 30px;
}
.user-icon {
  height: 20px;
  margin: 5px 0 0 5px;
}

h5 {
  margin: 7px 7px 0 0;
}

a:hover {
  cursor: pointer;
  color: white;
}

ul {
  list-style: none;
  padding: 0;
}
li {
  padding-left: 1em;
  color: #9a9a9a;
}

.sidebar {
  min-width: 175px;
  max-width: 175px;
  min-height: 100% !important;
  flex: 1;
  font-size: 18px;
  line-height: 3;
  padding-top: 5em;
  background: #212121;
  color: white;
  list-style: none;
  text-align: left;
  font-weight: 500;
}

.sidebar-icon {
  height: 25px;
  margin: 0px 7px -4px -5px;
}

.active {
  background: #4e4e4e;
}
.content {
  display: flex;
  flex: 1;
  flex-wrap: wrap;
  margin-top: 2em;
}

@media screen and (max-width: 700px) {
  #app {
    display: block;
  }
  .sidebar {
    max-width:100%;
    padding: .5em 0 0 0;
  }
}
</style>
