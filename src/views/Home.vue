<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://m.media-amazon.com/images/M/MV5BOTU4ZmNmMTktYzRkYS00Njc1LTg3ZjQtNDY4MmM0MTE5ZjhmXkEyXkFqcGdeQXVyMTA3MDk2NDg2._V1_FMjpg_UX452_.jpg" 
        alt="Tenet Poster" class="featured-img" />
        <div class="detail">
          <h3>Tenet</h3>
          <p>Um agente secreto embarca em uma missão perigosa para evitar o início da 
            Terceira Guerra Mundial.</p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="Busque filmes, séries, e mais..." v-model="search" />
      <input type="submit" value="Buscar" />
    </form>


   <!-- HTML lista de filmes que será mostrada no retorno da busca  -->
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js'

export default {
  setup () {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<!-- CSS dos componente de Ui da página -->
<style lang="scss">
.home {
  .feature-card {
    position: relative;
/* CSS imagem destaque */
    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;

      position: relative;
      z-index: 0;
    }
/* texto detalhes */
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      h3 {
        color:#FFF;
        margin-bottom: 16px;
      }

      p {
        color: #FFF;
      }
    }
  }

/* campo de busca */
  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
          color: #fff;
          background-color:#0f0f1064;
          border-radius: 8px;
          font-size: 20px;
          padding: 10px 16px;
          margin-bottom: 15px;
          transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
            box-shadow: 0px 3px 6px rgba(0,0,0, 0.2);
        }
      }

      /* botõa enviar */

      &[type="submit"] {
         width: 100%;
          max-width: 400px;
          background-color: #000;
          padding: 16px;
          border-radius: 8px;
          color: #fff;
          font-size: 20px;
          text-transform: uppercase;
          transition: 0.4s;

        &:active {
          background-color: #959b6b;
        }
      }
    }
  }
 /* lista de filmes */
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #f5c518e7;
            color: #FFF;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #000;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year {
            color: #AAA;
            font-size: 14px;
          }

          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>