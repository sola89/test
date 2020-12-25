<template>
  <!-- Блок приложения -->
  <div id="app">
    <div class="sidebar">
      <div class="container">
        <div class="logo-text">Admin Test</div>
      </div>
    </div>
    <!-- view роутера -->
    <router-view />
  </div>
</template>

<script>
export default {
  name: "app",
};
</script>