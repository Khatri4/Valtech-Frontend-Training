<script setup>
import { ref } from "vue";

let lady = ref("");
let ladyAvengers = ref([
  {
    title: "Wasp",
    firstname: "Janet",
    lastname: "Van Dyne",
    movies: [
      { title: "Ant-Man", year: 2015 },
      { title: "Ant‑Man and the Wasp", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Scarlet Witch",
    firstname: "Wanda",
    lastname: "Maximoff",
    movies: [
      { title: "Captain America: The Winter Soldier", year: 2014 },
      { title: "Avengers: Age of Ultron", year: 2015 },
      { title: "Captain America: Civil War", year: 2016 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
      { title: "Doctor Strange in the Multiverse of Madness", year: 2022 },
    ],
  },
  {
    title: "Black Widow",
    firstname: "Natasha",
    lastname: "Romanoff",
    movies: [
      { title: "Iron Man 2", year: 2010 },
      { title: "Avengers", year: 2012 },
      { title: "Captain America: The Winter Soldier", year: 2014 },
      { title: "Avengers: Age of Ultron", year: 2015 },
      { title: "Captain America: Civil War", year: 2016 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Captain Marvel",
    firstname: "Carol",
    lastname: "Danvers",
    movies: [
      { title: "Captain Marvel", year: 2019 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Gamora",
    firstname: "Gamora Zen",
    lastname: "Whoberi Ben Titan",
    movies: [
      { title: "Guardians of the Galaxy", year: 2014 },
      { title: "Guardians of the Galaxy Vol. 2", year: 2017 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Shuri",
    firstname: "Shuri",
    lastname: "Princess",
    movies: [
      { title: "Black Panther", year: 2018 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
      { title: "Black Panther: Wakanda Forever", year: 2022 },
    ],
  },
]);

let result = ref(ladyAvengers.value);

let searchLady = () => {
  let search = lady.value.toLowerCase();
  result.value = ladyAvengers.value.filter((avenger) => {
    return (
      avenger.firstname.toLowerCase().includes(search) ||
      avenger.lastname.toLowerCase().includes(search) ||
      avenger.title.toLowerCase().includes(search) ||
      avenger.movies.some((movie) => movie.title.toLowerCase().includes(search))
    );
  });
};
</script>

<template>
  <div class="container">
    <h1>Lady Avengers</h1>
    <label>Search Lady Avenger: </label>&nbsp;
    <input type="text" v-model="lady" />
    <button @click="searchLady">Search</button>
    <hr />

    <div v-for="(ladyAve, idx) in result" :key="idx">
      <h1>Lady Avenger: {{ ladyAve.title }}</h1>
      <p>Title: {{ ladyAve.title }}</p>
      <p>First Name: {{ ladyAve.firstname }}</p>
      <p>Last Name: {{ ladyAve.lastname }}</p>
      <p>Full Name: {{ ladyAve.firstname }} {{ ladyAve.lastname }}</p>

      <h2>Movies of Lady Avenger - {{ ladyAve.movies.length }} Movies</h2>
      <ul>
        <li v-for="(movie, idx) in ladyAve.movies" :key="idx">
          {{ movie.title }} - {{ movie.year }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 700px;
  margin: 40px auto;
  padding: 20px;
  background-color: #39f2ff3f;
  border-radius: 10px;
  font-family: "Segoe UI";
}

h1 {
  color: #000000;
  text-align: center;
  margin-bottom: 20px;
}

label {
  font-weight: 600;
  color: #031e39;
}

input[type="text"] {
  padding: 8px 12px;
  font-size: 16px;
  margin: 10px 0;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: calc(100% - 24px);
  box-sizing: border-box;
}

button {
  padding: 8px 16px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-left: 10px;
}

button:hover {
  background-color: #2980b9;
}

hr {
  margin: 20px 0;
}

p {
  margin: 5px 0;
  color: #0a243d;
}

ul {
  list-style: disc;
  padding-left: 20px;
  margin-top: 10px;
  margin-bottom: 20px;
}

li {
  margin-bottom: 5px;
  color: #0b3641;
}

h2 {
  margin-top: 15px;
  color: #062022;
  font-size: 18px;
}
</style>
