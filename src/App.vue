<template>
  <div id="app">
    <div class="wrapper">
      <nav class="navbar">
        <ul>
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/post">Post</router-link></li>
          <li><router-link to="/todos">Todos</router-link></li>
          <li><router-link to="/albums">Albums</router-link></li>
        </ul>
      </nav>
    </div>
    <div class="content">
      <router-view/>
    </div>
  </div>
</template>

<style>
body, html {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  font-family: Arial, sans-serif;
  background: url('https://your-image-url.jpg') no-repeat center center fixed;
  background-size: cover;
  overflow:scroll;
}

#app {
  display: flex;
  flex-direction: column;
  height: 100%;
  background: rgba(25, 157, 11, 0.5);
}

.wrapper {
  margin-bottom: 20px;
}

.navbar {
  background-color: rgba(105, 220, 113, 0.8);
  padding: 10px 0;
}

.navbar ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  justify-content: center;
}

.navbar li {
  padding: 10px 20px;
}

.navbar li a {
  color: white;
  text-decoration: none;
  display: block;
  font-size: 18px;
  transition: background-color 0.3s, color 0.3s;
}

.navbar li a:hover {
  background-color: #575757;
  color: #fff;
}

.content {
  flex: 1;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url('https://rencanamu.id/assets/file_uploaded/editor/1529158361-studio-ghi.jpg');
  background-size: cover;
  border-radius: 10px;
  margin: 20px;
  background-size:100%;
}

</style>
