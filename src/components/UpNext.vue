<template>
  <div class="main">
    <h1>Up Next</h1>
    <!-- map through queue data for song item -->
    <!-- feels like a syntaxical nightmare but its so easy wtf -->
    <div class="list">
      <div class="album" v-for="(item, index) in upNext" :key="index">
        <img class="artwork" :src="item.artwork_large" />
        <div class="info">
          <div>
            <h3>{{ item.song }}</h3>
            <p>{{ item.artist }}</p>
          </div>
          <div class="vote">
            <img
              src="../assets/icons/thumbs-down-regular.svg"
              class="like"
              v-on:click="thumbsDown(item.pick_id)"
            />
            <img
              src="../assets/icons/thumbs-up-regular.svg"
              class="like"
              v-on:click="thumbsUp(item.pick_id)"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { headers } from "../headers";
import Vue from "vue";
import VueToast from "vue-toast-notification";
import "vue-toast-notification/dist/theme-sugar.css";
Vue.use(VueToast);

export default {
  name: "UpNext",
  props: {
    upNext: Array,
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

.like {
  height: 20px;
  width: 20px;
  margin-left: 15px;
}
.like:hover {
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

@media screen and (max-width: 700px) {
  h3 {
    line-height: 1;
  }
}
</style>
