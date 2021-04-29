<template>
  <footer class="nowPlaying">
    <img class="album" :src="nowPlaying.artwork_small" />
    <div class="info">
      <h3>{{ nowPlaying.song }}</h3>
      <p>{{ nowPlaying.artist }}</p>
    </div>
    <div class="vote">
      <button class="like">
        <img
          class="thumb-down"
          src="../assets/icons/thumbs-down-regular.svg"
          v-on:click="thumbsDown(nowPlaying.pick_id)"
        />
      </button>
      <button class="like">
        <img
          class="thumb-up"
          src="../assets/icons/thumbs-up-regular.svg"
          v-on:click="thumbsUp(nowPlaying.pick_id)"
        />
      </button>
    </div>
    <!-- add duration / time remaining counter -->
  </footer>
</template>

<script>
import { headers } from "../headers";
import Vue from "vue";
import VueToast from "vue-toast-notification";
import "vue-toast-notification/dist/theme-sugar.css";
Vue.use(VueToast);

export default {
  name: "NowPlaying",
  props: {
    nowPlaying: Object,
  },
  methods: {
    thumbsUpToast() {
      Vue.$toast.open({
        message: "+1 Like",
        type: "success",
      });
    },
    thumbsDownToast() {
      Vue.$toast.open({
        message: "+1 Dislike",
        type: "error",
      });
    },
    thumbsUp(pick_id) {
      fetch(`https://api.rockbot.com/v3/engage/vote_up?pick_id=${pick_id}`, {
        method: "POST",
        headers,
      })
        .then((res) => res.json())
        .then(() => this.thumbsUpToast());
    },
    thumbsDown(pick_id) {
      fetch(`https://api.rockbot.com/v3/engage/vote_down?pick_id=${pick_id}`, {
        method: "POST",
        headers,
      })
        .then((res) => res.json())
        .then(() => this.thumbsDownToast());
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nowPlaying {
  display: flex;
  align-items: center;
  margin-left: -12em;
  width: 125%;
  height: 9em;
  background: #4e4e4e;
  color: white;
  padding: 1em 1em 1em 3em;
  bottom: 0;
  position: absolute;
}

.album {
  height: 90px;
  width: 90px;
  background: black;
}

.info {
  margin-left: 1em;
  font-size: 16px;
  line-height: 0.5;
}

.vote {
  display: flex;
  margin-left: 25%;
}

.like {
  height: 75px;
  width: 75px;
  /* background: tomato; */
  margin: 0 1em;
  border: 5px solid lightgrey;
  border-radius: 100%;
}

.like:focus {
  outline: none;
}

.like:hover {
  cursor: pointer;
}

.thumb-down {
  height: 40px;
  margin: 5px 0 0 5px;
  /* background: tomato; */
}

.thumb-up {
  height: 40px;
  margin: 0px 0 0 5px;
  /* background:palegreen; */
}

h3 {
  line-height: 1;
}

@media screen and (max-width: 700px) {
  .nowPlaying {
    margin: 0;
    width: 100%;
  }

  p {
    line-height: 1;
  }
  .thumb-down,
  .thumb-up,
  .like {
    height: 20px;
    width: 20px;
    background: none;
    border: none;
  }

  .vote {
    margin-left: 15%;
  }
}
</style>
