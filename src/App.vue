<template>
  <h2>Free URL Shortener</h2>

  <form @submit.prevent="submit">
    <input v-model="longUrl" type="text" /> |

    <input type="submit" value="Submit" />
  </form>

  <div v-if="shortUrl">
    <input id="shortUrl" type="text" :value="this.shortUrl" />
    <button @click="copy">Copy Url</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",

  data() {
    return {
      longUrl: "",
      shortUrl: null,
    };
  },

  methods: {
    async submit() {
      const data = await axios.post("https://shlyit.herokuapp.com/", {
        url: this.longUrl,
      });
      this.shortUrl = data.data;
    },

    copy() {
      const text = document.getElementById("shortUrl");

      text.select();

      navigator.clipboard.writeText(text.value);
    },
  },
};
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
