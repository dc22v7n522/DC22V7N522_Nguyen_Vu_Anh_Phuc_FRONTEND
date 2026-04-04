<template>
  <div class="login-page">
    <div class="login-card">
      <h3>Đăng nhập</h3>
      <form @submit.prevent="handleLogin">
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
          <button type="submit" class="btn btn-primary">Đăng nhập</button>
          <button
            type="button"
            class="btn btn-secondary"
            @click="$router.push({ name: 'register' })"
          >
            Đăng ký
          </button>
        </div>

        <div class="social-group mt-3">
          <a
            href="http://localhost:3000/api/auth/google"
            class="btn btn-danger w-100 mb-2"
          >
            <i class="fab fa-google"></i> Đăng nhập Google
          </a>

          <a
            href="http://localhost:3000/api/auth/facebook"
            class="btn btn-facebook w-100"
          >
            <i class="fab fa-facebook-f"></i> Đăng nhập Facebook
          </a>
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
      email: "",
      password: "",
    };
  },
  methods: {
    // LOGIC ĐĂNG NHẬP
    async handleLogin() {
      try {
        const response = await axios.post(
          "http://localhost:3000/api/auth/login",
          {
            email: this.email,
            password: this.password,
          },
          { withCredentials: true },
        );

        if (response.data) {
          alert("Đăng nhập thành công!");
          window.location.href = "/";
        }
      } catch (error) {
        console.error(error);
        alert("Sai email hoặc mật khẩu!");
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

.social-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 15px;
}

.btn-facebook {
  background-color: #1877f2;
  color: white;
  border: none;
}

.btn-facebook:hover {
  background-color: #166fe5;
  color: white;
}

.w-100 {
  width: 100%;
}
.mb-2 {
  margin-bottom: 8px;
}
</style>
