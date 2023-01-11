<script setup>
import axios from "axios";
import { ref } from "vue";

const users = ref("");
const onClickFetchApi = async () => {
  await axios
    .get("https://jsonplaceholder.typicode.com/users")
    .then((response) => (users.value = response.data));
};
</script>

<template>
  <h1>api叩いて、戻り値から自己紹介カード作ってみる</h1>
  <button @click="onClickFetchApi">取得！</button>
  <div class="wrapper" v-if="users">
    <div v-for="user in users" :key="user.id">
      <div class="container">
        <img src="https://picsum.photos/400/300" />
        <p>{{ user.name }}</p>
        <p class="highlights">{{ user.email }}</p>
      </div>
    </div>
  </div>
  <RouterView />
</template>

<style scoped>
img {
  width: 80px;
  height: 80px;
  border-radius: 50%;
}
.wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  max-width: 1280px;
  margin: 0 auto;
}
.container {
  background: hsl(136, 74%, 85%);
  width: 200px;
  padding: 10px;
  border-radius: 10px;
  margin: 10px;
}
.highlights {
  background: rgb(39, 151, 140);
  color: #fff;
}
</style>
