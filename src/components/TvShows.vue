/* eslint-disable max-len */
<template>
  <div class="hello">
    <h1>Search</h1>
    <b-form-input
      v-model="searchQuery"
      @keyup="searchMovie"
      placeholder="Enter your search keyword"
    ></b-form-input>
    <div v-for="show in filteredResult" :key="show.id">
      <b-card
        :title="show.show.name"
        :img-src="show.show.image.medium"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem;"
        class="mb-2"
      >
        <b-card-text>Rating : {{ show.show.rating.average }}</b-card-text>
        <b-button
          tag="router-link"
          target="_blank"
          :to="`/show-detail/${show.show.id}`"
          variant="primary"
        >Go somewhere</b-button>
      </b-card>
    </div>
    <hr />
    <h1>Shows</h1>

    <hr />
    <h1>Drama</h1>
    <div v-for="(show, index) in movieDramaGenre" :key="show.id">
      <div v-if="index < 4">
        <b-card
          :title="show.name"
          :img-src="show.image.medium"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2"
        >
          <b-card-text>Rating : {{ show.rating.average }}</b-card-text>
          <b-button
            tag="router-link"
            target="_blank"
            :to="`/show-detail/${show.id}`"
            variant="primary"
          >See more</b-button>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "TvShows",
  data: () => ({
    movies: [],
    genres: [],
    result: [],
    searchQuery: "",
  }),
  mounted() {
    this.fetchShows();
  },
  computed: {
    filteredResult() {
      let { result } = this;
      const { searchQuery } = this;

      if (!searchQuery) {
        return result;
      }

      result = result.filter((item) => item);
      return result;
    },
    movieDramaGenre() {
      let dramaGenre = this.movies.filter((m) =>
        m.genres.find((g) => g.toLowerCase() === "drama")
      );

      return dramaGenre;
    },
  },
  methods: {
    searchMovie() {
      axios
        .get(`http://api.tvmaze.com/search/shows?q=${this.searchQuery}`)
        .then((response) => {
          this.result = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },

    fetchShows() {
      axios
        .get("http://api.tvmaze.com/shows")
        .then((response) => {
          this.movies = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
