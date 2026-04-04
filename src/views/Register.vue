<template>
  <div class="login-page">
    <div class="login-card">
      <h3>Đăng ký tài khoản</h3>
      <form @submit.prevent="handleRegister">
        <div class="form-group">
          <input
            type="text"
            class="form-control"
            placeholder="Tên hiển thị"
            v-model="displayName"
            required
          />
        </div>
        <div class="form-group">
          <input
            type="email"
            class="form-control"
            placeholder="Email"
            v-model="email"
            required
          />
        </div>
        <div class="form-group">
          <input
            type="password"
            class="form-control"
            placeholder="Mật khẩu"
            v-model="password"
            required
          />
        </div>

        <div class="button-group">
          <button type="submit" class="btn btn-success w-100">
            Xác nhận Đăng ký
          </button>
        </div>
        <div class="mt-3">
          <a href="#" @click.prevent="$router.push({ name: 'login' })"
            >Đã có tài khoản? Đăng nhập</a
          >
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      displayName: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async handleRegister() {
      try {
        await axios.post("http://localhost:3000/api/auth/register", {
          displayName: this.displayName,
          email: this.email,
          password: this.password,
        });
        alert("Đăng ký thành công! Mời bạn đăng nhập ");
        this.$router.push({ name: "login" });
      } catch (error) {
        alert(
          "Lỗi rồi: " + (error.response?.data?.message || "Không đăng ký được"),
        );
      }
    },
  },
};
</script>

<style scoped>
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80vh;
}
.login-card {
  width: 400px;
  padding: 30px;
  border: 1px solid #ddd;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
.form-group {
  margin-bottom: 15px;
}
.button-group {
  display: flex;
  justify-content: space-between;
  gap: 5px;
}
.btn {
  flex: 1;
  font-size: 14px;
}
.w-100 {
  width: 100%;
}
</style>
