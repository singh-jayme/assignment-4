<script setup>
import { ref } from "vue";
import axios from "axios";

const movies=ref("")
const response = ref(null);

const getMovie = async () => {
  response.value = (
    await axios.get(`https://api.themoviedb.org/3/movie/${movie.value}`, {
      params: {
        api_key: "ab590dbfc1eb546b5263a30c390d2d07",
      },
    })
  ).data;
};
</script>

<template>
  <body>
    <div class="list">
      <select v-model="movies">
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
      <button @click="getMovie">Get</button>
    </div>
    <div v-if="response">
      <h1></h1>
      <h2></h2>
      <p></p>
    </div>
  </body>
</template>
 
<style scoped>
body {
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