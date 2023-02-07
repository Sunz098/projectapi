<script setup>
import { ref } from "vue";
import axios from "axios";

const url = ref(
  "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=PSQoqe2gAua3D66U9kAZH97WrMB9HWUb64Gtjdxs"
);
const userdata = ref([]);

function loadUser() {
  axios
    .get(url.value)
    .then((response) => {
      userdata.value = response.data;
    })
    .catch((err) => {
      console.log(err);
    });
}
</script>

<template>
  <div>
    <h1>User View</h1>
    <h2>แสดงรายชื่อ User</h2>
    <button @click="loadUser()">Load user data</button>
    {{ userdata }}
    <!--<ul>
      <li v-for="user in userdata" :key="user.id">
        {{ user.earth_date }}
        

      </li>
    </ul>-->
  </div>

  <div></div>
</template>
