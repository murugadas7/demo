<template>
  <div class="ui container">
    <p class="error-text">404</p>
    <div>
      <span>Take me</span>
      <NuxtLink to="/">Home</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
.container {
  height: viewport;
  background-color: rgba(0, 255, 0, 0.5);
  
}
.error-text {
  font-size: 130px;
}
</style>
