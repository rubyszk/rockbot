<template>
  <div id="app">
    <h1>Rockbot Lite</h1>
    <img alt="Vue logo" src="./assets/logo.png">
  </div>
</template>

<script>
//header
//footer - now playing
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  
  // components: {
  //   HelloWorld
  // }
  data() {
    return {
      // isLoading: false,
      nowPlaying: {},
      upNext: {},
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
      // API Call also fetches Queue
      // fetch from url
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

    },
    mounted() {
      // Call on mount to fetch data
      // (useEffect/componentDidMount)

      this.fetchNowPlaying();
      this.fetchBrowse();
      this.fetchTopArtists();
    }


  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
