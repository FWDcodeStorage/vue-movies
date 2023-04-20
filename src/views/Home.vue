<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt3896198">
        <img
          src="https://m.media-amazon.com/images/M/MV5BNjM0NTc0NzItM2FlYS00YzEwLWE0YmUtNTA2ZWIzODc2OTgxXkEyXkFqcGdeQXVyNTgwNzIyNzg@._V1_SX300.jpg"
          alt="poster" class="feature-img" />
        <div class="details">
          <h3>Guardians of the Galaxy Vol. 2</h3>
          <p>
            The Guardians struggle to keep together as a team while dealing with
            their personal family issues, notably Star-Lord's encounter with his
            father the ambitious celestial being Ego.
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search" />
      <input type="submit" value="Search" @click.prevent="SearchMovies" />
    </form>

    <div class="movie-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="movie-poster">
            <img :src="movie.Poster" :alt="movie.Title">
            <div class="type">
              {{ movie.Type }}
            </div>
          </div>
          <div class="detail">
            <div>
              <p class="year"> Year: {{ movie.Year }}</p>
              <h3>{{ movie.Title }}</h3>
            </div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from "vue";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${process.env.VUE_APP_API_KEY}&s=${search.value}`)
          .then((res) => res.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return {
      search, movies, SearchMovies
    };
  },
};
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .feature-img {
      display: block;
      width: 100%;
      height: 40vh;
            object-fit: cover;

      position: relative;
      z-index: 0;
    }

    .details {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.5);
      padding: 15px;
      z-index: 1;

      h3 {
        color: #fff;
        margin-bottom: 15px;
        font-size: 1.1rem;
        letter-spacing: 0.03rem;
      }

      p {
        font-size: 0.9rem;
        letter-spacing: 0.02rem;
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 15px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: #fff;
        background: #496583;
        font-size: 20px;
        padding: 10px 15px;
        border-radius: 5px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder {
          color: #d2d2d2;
        }

        &:focus {
          box-shadow: 8px 3px 6px rgba(0, 0, 0, 0.3);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 500px;
        background-color: rgb(3, 193, 246);
        padding: 15px;
        border-radius: 5px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #3b8870;
        }
      }
    }
  }

  .movie-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 5px;

    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 15px 5px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
        cursor: pointer;

        .movie-poster {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 300px;
            object-fit: cover;
          }


          .type {
            position: absolute;
            padding: 5px 15px;
            background-color: rgb(3, 193, 246);
            color: #fff;
            top: 15px;
            left: 0;
            text-transform: capitalize;
          }

        }

        .detail {
          background-color: #496583;
          padding: 15px 5px;
          flex: 1 1 100%;
          border-radius: 0px 0px 5px 5px;

          .year {
            color: #b5b5b5;
          }
        }
      }
    }
  }
}
@media only screen and (min-width:768px) {
  .home{
    .feature-card{
      .feature-img{
        
      }

      .details{
        h3{
          font-size: 1.5rem;
        }
        p{
          font-size: 1rem;
        }
      }
    }

    .search-box{
      padding: 25px;
      input[type="text"]{
        padding: 15px 25px;
        font-size: 26px;
      }

      input[type="submit"] {
        max-width: 700px;
      }
    }

    .movie-list{
      margin: 0 25px;

      .movie-link{

        .movie-poster{

          img {
            max-height: 500px !important;
          }
        }
      }
    }
  }
}

@media only screen and (min-width:1024px){
  h1{
    font-size: 3rem;
  }
  h3{
    font-size: 1.8rem;
  }
  p{
    font-size: 1.1rem;
  }
  .home{
    .feature-card{
      .feature-img{
        min-height: 50vh;
        max-height: 65vh;
        
      }

      .details{
        h3{
          font-size: 1.8rem;
        }
        p{
        font-size: 1.2rem;
  }
      }
    }

    .search-box{
      padding: 25px;
      input[type="text"]{
        font-size: 30px;
      }

      input[type="submit"] {
        max-width: 90vw;
        font-size: 30px;
      }
    }

    .movie-list{
      margin: 0 25px;

      .movie-link{
        
        .movie-poster{

          img {
            height: 500px !important;
          }
        }
      }
    }
  }
}
</style>
