<script setup>
import { ref } from 'vue'
import axios from "axios";
 
const getMovies1 = async () => {
  let movieBG= document.getElementById("movieBG");
  movieBG.innerHTML="";
  let filmSelect = document.getElementById("filmSelect")
  const movieData = await getData (`https://api.themoviedb.org/3/search/movie/`, {
    params: {
      api_key: "8d992bf093d92b23f2529662f9291664",
        query: filmSelect.value,
    }
  });
 
  if (movieData.data.results.length<1) {
    return;
  }
 
  let movie= movieData.data.results[0];
    const extraData = await getData(`https://api.themoviedb.org/3/movie/${movie.id}`, {
      params: {
        api_key: "8d992bf093d92b23f2529662f9291664",
        append_to_response: "videos",
      }
    });
 
    const trailer = extraData.data.videos.results.filter((video) => video.type === "Trailer").at(0).key;
    const h1 = document.createElement('h1');
    const h2 = document.createElement('h2');
    const p = document.createElement('p');
    const img = document.createElement('img');
    const iframe = document.createElement('iframe');
 
    h1.innerHTML = `${movie.title} -- ${movie.release_date}`;
    h2.innerHTML = `${movie.overview}`;
    p.innerHTML = `Runtime: ${extraData.data.runtime} minutes <br> Popularity: ${movie.popularity} <br> Average Rating: ${movie.vote_average} -- Based on: ${movie.vote_count} votes <br> Budget: $${extraData.data.budget} <br> Revenue: $${extraData.data.revenue} <br> Original Language: ${movie.original_language}`;
    img.src = `https://image.tmdb.org/t/p/w500${movie.poster_path}`
    iframe.src = `https://www.youtube.com/embed/${trailer}`;
 
    //DOM
    movieBG.append(h1)
    movieBG.append(h2)
    movieBG.append(p);
    movieBG.append(img);
    movieBG.append(iframe);
  }
 
;
 
getMovies1();
</script>
 
<template>
  <div label="bg">
      <div class="list">
        <select name="movies" id="filmSelect">
          <option value="493922">Hereditary</option>
          <option value="496243">Parasite</option>
          <option value="400617">Phantom Thread</option>
          <option value="103">Taxi Driver</option>
          <option value="115">The Big Lebowski</option>
          <option value="503919">The Lightouse</option>
          <option value="68722">The Master</option>
          <option value="37799">The Social Network</option>
          <option value="473033">Uncut Gems</option>
          <option value="244786">Whiplash</option>
        </select>
        <br><br>
        <button onclick="getMovies1()">Get</button>
          <div id="movieBG">
          </div>
      </div>
  </div>
</template>
 
<style scoped>
div.bg {
  background-color:black;
  text-align: center;
}
 
p {
  text-align: center;
  color: lightblue;
  font-size: 25px;
  font-weight: bold;
}
 
h1 {
  text-align: center;
  font-size: 45px;
  color: yellow;
}
 
h2 {
  color: rgb(173, 228, 230);
  font-size: 30px;
  font-weight: bold;
}
 
div.list {
text-align: center;
font-size: 40px;
color: lightgreen;
}
 
img {
  height: 430px;
  padding-right: 30px;
}
 
iframe {
  aspect-ratio: 16/9;
  height: 430px;
}
 
.button{
  height: 32px;
  width: 130px;
  font-size: 20px;
  font-family: "Times New Roman", Times, serif;
}
</style>
>