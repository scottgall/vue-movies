<template>
  <ul>
    <li v-for="movie in movies">
      <Movie :movie="movie" />
    </li>
  </ul>
</template>

<script>
import Movie from './Movie.vue';
export default {
  name: 'MoviesList',
  data() {
    return {
      movies: []
    }
  },
  beforeCreate() {
    console.log('before create');    
  },
  created: function() {
    console.log('created');
    this.fetchData();
  },
  beforeMount() {
    console.log('before mount');
  },
  mounted() {
    console.log('mounted');    
  },
  beforeUpdate() {
    console.log('before update');    
  },
  updated() {
    console.log('updated');
  },
  methods: {
    fetchData: async function() {
      try {
        const res = await fetch(
          'https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=03217c780beb981d10b0d7ef19d8ab4b'
        );
        const movies = await res.json();
        this.movies = movies.results;
      } catch (e) {
        console.log(e);
      }
    }
  },
  components: {
    Movie
  }
}
</script>

<style scoped>
ul {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
}
li {
  padding: 1rem;
}
</style>