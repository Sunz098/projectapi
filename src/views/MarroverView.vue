<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const url = ref(
  "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=PSQoqe2gAua3D66U9kAZH97WrMB9HWUb64Gtjdxs"
);
const photos = ref();

function loaddata() {
  axios
    .get(url.value)
    .then((response) => {
      photos.value = response.data.photos;
    })
    .catch((err) => {
      console.log(err);
    });
}

onMounted(() => {
  loaddata();
});
</script>

<template>
  <div class="container">
    <header>Picture mar-rover</header>

    <div class="teamcard">
      <div v-for="(data, n) in photos" :key="n">
        <div class="card" style="width: 18rem">
          <img :src="data.img_src" class="card-img-top" alt="..." />
          <div class="card-body">
            <p class="card-text">
              date: {{ data.earth_date }} id:{{ data.id }} <br />
              sol: {{ data.sol }} <br />
              camera <br />
              id: {{ data.camera.id }} name: {{ data.camera.name }} rover_id :
              {{ data.camera.rover_id }} <br />
              rover <br />
              rover_id : {{ data.rover.id }} name: {{ data.rover.name }} <br />
              landing_date: {{ data.rover.landing_date }} launch_date:{{
                data.rover.lanch_date
              }}
              status:{{ data.rover.status }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 35px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}

.teamcard {
  display: grid;
  justify-content: center;
  align-items: center;
  grid-template-columns: 1fr 1fr 1fr;
  margin-top: 20px;
}
</style>
