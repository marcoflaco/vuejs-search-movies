
<template>
  <!-- search template -->
  <div>
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
    <!-- show genre drama -->
    <hr />
    <div>
      <h1>Drama</h1>
      <div class="movie__rows">
        <div v-for="(show, index) in movieDramaGenre" :key="show.id" class="movie__row">
          <div v-if="index < 4">
            <img :src="show.image.medium" />
            <p>{{show.name}}</p>
            <b-card-text>Rating : {{ show.rating.average }}</b-card-text>
            <b-button
              tag="router-link"
              target="_blank"
              :to="`/show-detail/${show.id}`"
              variant="primary"
            >See more</b-button>
          </div>
        </div>
      </div>
    </div>
    <!-- show genre action -->
    <div>
      <h1>Music</h1>
      <div class="movie__rows">
        <div v-for="(show, index) in tvMusicGenre" :key="show.id" class="movie__row">
          <div v-if="index < 4">
            <img :src="show.image.medium" />
            <p>{{show.name}}</p>
            <b-card-text>Rating : {{ show.rating.average }}</b-card-text>
            <b-button
              tag="router-link"
              target="_blank"
              :to="`/show-detail/${show.id}`"
              variant="primary"
            >See more</b-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import "../scss/components/tvShows.scss";
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
    //filter result for search
    filteredResult() {
      let { result } = this;
      const { searchQuery } = this;

      if (!searchQuery) {
        return result;
      }

      result = result.filter((item) => item);
      return result;
    },
    //filter from movies array to get genre drama
    movieDramaGenre() {
      let dramaGenre = this.movies.filter((m) =>
        m.genres.find((g) => g.toLowerCase() === "drama")
      );

      return dramaGenre;
    },
    //filter from movies array to get genre music
    tvMusicGenre() {
      let musicGenre = this.movies.filter((movie) =>
        movie.genres.find((g) => g.toLowerCase() === "music")
      );

      return musicGenre;
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
