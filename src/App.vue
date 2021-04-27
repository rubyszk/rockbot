<template>
  <div id="app">
    <!-- <div class="header">
      <h1> Rockbot HQ</h1>
  
    </div> -->
    <div class="sidebar">
      <li> Home </li>
      <li> Search </li>
      <li> What's Hot </li>
    </div>    

    <div class="content">
    <Search/>
    <UpNext
      :upNext="upNext"
    />
    <NowPlaying
      :nowPlaying="nowPlaying"
    />
    </div>
  </div>
</template>

<script>
//header
//footer - now playing
import NowPlaying from './components/NowPlaying';
import UpNext from './components/UpNext';
import Search from './components/Search';
import { headers } from './headers';

export default {
  name: 'App',
  
  components: {
    NowPlaying,
    UpNext,
    Search
  },
  data() {
    return {
      // isLoading: false,
      nowPlaying: {},
      upNext: [],
      browseArtists: {},
      trendingArtists: {},
      searchResults: {}
    }
  },
  computed: {
    window: () => window,
    isPlaying() {
      return `${this.nowPlaying}`
    },
  },
  methods: {
    fetchNowPlaying(){ 
      console.log(process.env.VUE_APP_API_KEY)
      // API call fetches now playing and queue data
      fetch("https://api.rockbot.com/v3/engage/now_playing?queue=1", {
        headers
      }).then((res) => res.json())
      .then((data) => {
        this.nowPlaying = data.response.now_playing
        this.upNext = data.response.queue
        console.log(data.response)
      })
      // 2ab742c917f872aa88644bc8f995e03159b2
      // .then((res) => res.json())
      //.then((data)=> {
        //this.nowPlaying = data.res.now_playing
      // })
      // fetch every 30 seconds
      // window.setInterval(() => {
        // this.nowPlaying()
      // }, 30000)
    },
    sayHello(){
      window.setInterval(() => {
        console.log('hellooooo')
      }, 1000)
    },
    fetchBrowse(){
      // API Call

    },
    fetchTopArtists(){
      // API Call

    }
  }, 
  mounted() {
      // Call on mount to fetch data
      // (useEffect/componentDidMount)

    this.fetchNowPlaying();
      // this.fetchBrowse();
      // this.fetchTopArtists();
  }
}
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
  color: #2c3e50;
}

.header {
  display: flex;
  justify-content: space-around;

}

.sidebar {
  min-width: 150px;
  max-width: 150px;
  min-height: 100%  !important;
  flex: 1;
  font-size: 18px;
  line-height: 3;
  padding: 5em 0 0 2em;
  background: #293546;
  color: white;
  list-style: none;
  text-align: left;
  font-weight: 500;
}

.content {
  display: flex;
  flex: 1;
  flex-wrap: wrap;
  margin-top: 2em;
}
</style>
