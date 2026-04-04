<script>
import AppHeader from "@/components/AppHeader.vue";
import axios from "axios";

export default {
  components: {
    AppHeader,
  },
  data() {
    return {
      isLoggedIn: false, // Biến này để biết đã login chưa
      user: null,
    };
  },

  async created() {
    try {
      const response = await axios.get(
        "http://localhost:3000/api/auth/status",
        {
          withCredentials: true, // Bắt buộc phải có để nhận diện Session
        },
      );
      if (response.data.loggedIn) {
        this.isLoggedIn = true;
        this.user = response.data.user;
      }
    } catch (error) {
      console.log("Chưa đăng nhập hoặc lỗi kết nối");
      this.isLoggedIn = false;
    }
  },
};
</script>

<template>
  <div id="app">
    <AppHeader :isLoggedIn="isLoggedIn" :user="user" />

    <div class="container mt-3">
      <router-view />
    </div>
  </div>
</template>

<style>
.page {
  max-width: 400px;
  margin: auto;
}
</style>
