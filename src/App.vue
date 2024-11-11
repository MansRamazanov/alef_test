<template>
  <header class="header">
    <div class="header-container">
      <div class="logo">
        <img src="./assets/img/logo/Frame 10.png" alt="logo" />
      </div>
      <nav>
        <RouterLink to="/" class="nav-item">Форма</RouterLink>
        <RouterLink to="/about" class="nav-item">Превью</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView class="main" />
  <footer class="footer">
    <div class="footer-text">all rights reserved</div>
  </footer>
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<style scoped>
.header {
  border-bottom: 1px solid #1111111a;
}

.header-container {
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  position: relative;
  max-width: 1280px;
  min-height: 76px;
}

.logo {
  position: absolute;
  left: 0;
}

.nav-item {
  text-decoration: none;
  color: #1111117a;
}

.nav-item:first-child {
  padding-right: 24px;
}

.nav-item:hover {
  color: #01a7fd;
  opacity: 0.6;
  transition: 0.3s cubic-bezier(0.36, 0.59, 0.76, 0.37);
}

.main {
  max-width: 1280px;
  margin: 0 auto;
}

.footer {
  background-color: #fafafa;
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
}

.footer-text {
  text-align: center;
  padding: 30px 0;
}
</style>
