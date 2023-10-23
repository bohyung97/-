

<template>
  <div class="app">
    <header>
      <h1>The <strong>Movie</strong>Database</h1>
      <form action="" class="search-box" v-on:submit.prevent="handleSearch">
      <input
        type="search"  
        class="search-field" 
        placeholder="search for an Movie..."
        required
        v-model="search_query"
        >
    </form>
    </header>
    <main>
      <div class="cards">
        <Card v-for="movie in movieList" :movie="movie" />
      </div>
    </main>    
  </div>
</template>

<script setup>
import Card from './components/Card.vue';
import { ref } from 'vue';

const movieList = ref([]);
const search_query = ref('')

const handleSearch = async () =>{
  movieList.value = await fetch(`https://api.themoviedb.org/3/search/movie?query=${search_query.value}&api_key=c8be101385677250558cd17949c8a721&include_adult=false&language=ko-kr&page=1`)
    .then(response => response.json())
    .then(data => data.results)

    
    console.log(movieList.value);
}

</script>


<style lang="scss">
$color:#313131;
%box-shadow {
  box-shadow: 0px 4px 8px rgba(0,0,0,0.15);
}

  * {
    margin: 0; 
    padding: 0;
    box-sizing: border-box;

    font-family: 'Fira Sans', sans-serif;
  }

  a { text-decoration: none;}

  header {
    padding-top: 50px;
    padding-bottom: 50px;    

    h1 {
      color: #888;
      font-size: 42px;
      font-weight:400;
      text-align: center;
      text-transform: uppercase;
      margin-bottom: 30px;

      strong {
        color: $color;
      }
      &:hover {
        color: $color;
      }
    }

    .search-box {
      display: flex;
      justify-content: center;
      padding-left: 30px;
      padding-right: 30px;

      .search-field {
        appearance: none;
        border: none;
        outline: none;
        background: none;

        background-color: #f3f3f3;
        @extend %box-shadow;

        display: block;
        width: 100%;
        max-width: 600px;
        padding: 15px;
        border-radius: 8px;

        color: $color;
        font-size: 20px;

        transition: 0.4s;

        &::placeholder {
          color: #aaa;          
        }
        &:focus,  &:valid {
            color: #fff;
            background-color: $color;
            @extend %box-shadow;
          }

      }
    }
  } 

  main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 16px;

    .cards {
      display: flex;
      flex-wrap: wrap;
      }
  }
</style>
