<script setup>
import { ref } from "vue";

import gamora from "@/components/images/gamora.jpg";
import wasp from "@/components/images/wasp.jpg";
import captain from "@/components/images/captain.jpg";
import wanda from "@/components/images/wanda.jpg";
import black from "@/components/images/black.jpg";
import shuri from "@/components/images/shuri.jpg";

const ladyAvengers = ref([
  {
    title: "Wasp",
    firstname: "Janet",
    lastname: "Van Dyne",
    image: wasp,
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
    image: wanda,
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
    image: black,
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
    image: captain,
    movies: [
      { title: "Captain Marvel", year: 2019 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Gamora",
    firstname: "Gamora Zen",
    lastname: "Whoberi Ben Titan",
    image: gamora,
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
    image: shuri,
    movies: [
      { title: "Black Panther", year: 2018 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
      { title: "Black Panther: Wakanda Forever", year: 2022 },
    ],
  },
]);
</script>

<template>
  <div class="container mt-5 position-relative">
    <h1 class="text-center mb-4">Lady Avengers</h1>

    <div
      id="ladyAvengerCarousel"
      class="carousel slide"
      data-bs-ride="carousel"
      data-bs-interval="2000"
      data-bs-wrap="true"
    >
      <div class="carousel-inner">
        <div
          class="carousel-item"
          v-for="(avenger, index) in ladyAvengers"
          :class="{ active: index === 0 }"
          :key="index"
        >
          <div
            class="d-flex flex-column flex-md-row align-items-center justify-content-center gap-4 p-4 bg-light rounded"
          >
            <div class="image-box text-center">
              <img
                :src="avenger.image"
                class="d-block rounded shadow"
                alt="Avenger Image"
                style="max-width: 200px; height: 300px; object-fit: cover"
              />
            </div>
            <div class="info-box text-start">
              <p><strong>Title:</strong> {{ avenger.title }}</p>
              <p>
                <strong>Full Name:</strong> {{ avenger.firstname }}
                {{ avenger.lastname }}
              </p>
              <h5 class="mt-3">Movies:</h5>
              <ul>
                <li v-for="(movie, idx) in avenger.movies" :key="idx">
                  {{ movie.title }} ({{ movie.year }})
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>

    <button
      class="carousel-control-prev custom-carousel-control"
      type="button"
      data-bs-target="#ladyAvengerCarousel"
      data-bs-slide="prev"
    >
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Previous</span>
    </button>

    <button
      class="carousel-control-next custom-carousel-control"
      type="button"
      data-bs-target="#ladyAvengerCarousel"
      data-bs-slide="next"
    >
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Next</span>
    </button>
  </div>
</template>

<style scoped>
.carousel-control-prev-icon,
.carousel-control-next-icon {
  background-color: rgba(0, 0, 0, 0.6);
  background-size: 100% 100%;
  border-radius: 50%;
  width: 40px;
  height: 40px;
}

.carousel-control-prev,
.carousel-control-next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 40px;
  height: 40px;
  z-index: 10;
}

.carousel-control-prev {
  left: 0;
}

.carousel-control-next {
  right: 0;
}

.container {
  max-width: 900px;
  height: 500px;
  margin: 40px auto;
  padding: 20px;
  background-color: #f5f7fa;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

h1 {
  color: #2c3e50;
  margin-bottom: 20px;
}

.image-box {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 200px;
}

.image-box img {
  max-width: 100%;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.info-box {
  flex: 1;
  min-width: 250px;
}

ul {
  margin-top: 10px;
  padding-left: 20px;
}

li {
  color: #34495e;
  margin-bottom: 5px;
}

.custom-carousel-control {
  top: 50%;
  transform: translateY(-50%);
  z-index: 2;
}
</style>
