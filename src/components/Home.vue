<template>
  <div class="home-container">
    <div class="home-content">
      <h1 class="home-title">WELCOME TO RUA </h1>
      <p class="home-description">Jelajahilah konten terbaik RUA</p>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
  }
}
</script>

<style>

.home-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: url('https://your-background-image-url.jpg') no-repeat center center fixed;
  background-size: cover;
}

.home-content {
  text-align: center;
  background: rgba(255, 255, 255, 0.8);
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.1);
}

.home-title {
  font-size: 48px;
  font-weight: bold;
  color: #333;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  font-family: 'Georgia', serif;
}

.home-description {
  font-size: 20px;
  color: #666;
  margin-bottom: 30px;
  line-height: 1.5;
  font-family: 'Georgia', serif;
}
</style>
