<template>
  <div>
    <search v-on:search-text="SearchText" />
    <joke
      v-for="joke in jokes"
      :key="joke.id"
      :id="joke.id"
      :joke="joke.joke"
    />
  </div>
</template>

<script>
import joke from "../../components/joke.vue";
import search from "../../components/search.vue";
import axios from "axios";
export default {
  layout: "default",
  components: {
    joke,
    search,
  },
  data() {
    return {
      jokes: [],
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };
    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);
      console.log(res.data);
      console.log("helloworld");
      this.jokes = res.data.results;
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async SearchText(text) {
      const config = {
        headers: {
          Accept: "application/json",
        },
      };
      try {
        const res = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        );
        console.log(res.data);
        console.log("helloworld");
        this.jokes = res.data.results;
      } catch (err) {
        console.log(err);
      }
    },
  },
  head() {
    return {
      title: "Funny Jokes ",
      meta: [
        { charset: "utf-8" },
        {
          hid: "description",
          name: "description",
          content: "Best place for thos who understand jokes",
        },
      ],
    };
  },
};
</script>

<style></style>
