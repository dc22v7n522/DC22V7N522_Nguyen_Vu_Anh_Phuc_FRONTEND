<template>
  <nav class="navbar navbar-expand navbar-dark bg-dark">
    <a href="/" class="navbar-brand">Ứng dụng Quản lý danh bạ</a>

    <div class="mr-auto navbar-nav">
      <li class="nav-item">
        <router-link :to="{ name: 'contactbook' }" class="nav-link">
          Danh bạ
          <i class="fas fa-address-book"></i>
        </router-link>
      </li>
    </div>

    <div class="navbar-nav ml-auto">
      <li class="nav-item d-flex align-items-center" v-if="isLoggedIn && user">
        <img
          :src="
            user.photos && user.photos.length > 0
              ? user.photos[0].value
              : user._json && user._json.picture
                ? user._json.picture
                : ''
          "
          alt="Avatar"
          class="rounded-circle mr-2"
          style="width: 30px; height: 30px; object-fit: cover"
        />
        <span class="text-white mr-2">{{ user.displayName }}</span>
      </li>

      <li class="nav-item" v-if="isLoggedIn">
        <a
          href="http://localhost:3000/api/auth/logout"
          class="nav-link btn btn-danger text-white ml-2"
        >
          Đăng xuất
        </a>
      </li>
      <li class="nav-item" v-else>
        <router-link :to="{ name: 'login' }" class="nav-link">
          Đăng nhập
        </router-link>
      </li>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    isLoggedIn: {
      type: Boolean,
      default: false,
    },
    // NHẬN DỮ LIỆU
    user: {
      type: Object,
      default: null,
    },
  },
};
</script>
