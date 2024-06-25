<template>
  <div class="album-container">
    <h2 class="heading">Albums</h2>
    <div v-if="albums.length" class="album-grid">
      <div v-for="album in albums" :key="album.id" @click="viewAlbum(album.id)" class="album-card">
        <div class="album-id">{{ album.id }}</div>
        <div class="album-title">{{ album.title }}</div>
      </div>
    </div>
    <div v-else class="no-albums">
      <p>No albums available.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useAlbumsStore } from '../stores/albums'
import { useRouter } from 'vue-router'

const albumsStore = useAlbumsStore()
const albums = ref([])
const router = useRouter()

const fetchAlbums = async () => {
  await albumsStore.fetchAlbums()
  albums.value = albumsStore.albums
}

const viewAlbum = (id) => {
  router.push(`/albums/${id}`)
}

onMounted(fetchAlbums)
</script>

<style scoped>
.album-container {
  padding: 40px;
  max-width: 1200px;
  margin: 50px auto;
  background: linear-gradient(to right, #c5e1a5, #aed581); /* Gradient of light green */
  border-radius: 15px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
  text-align: center;
}

.heading {
  color: #4caf50; /* Green header text color */
  font-weight: bold;
  margin-bottom: 30px;
  font-size: 28px;
  text-transform: uppercase;
  letter-spacing: 1px;
  position: relative;
  display: inline-block;
  padding-bottom: 10px;
}

.heading::after {
  content: '';
  width: 50%;
  height: 3px;
  background: #4caf50; /* Green underline */
  position: absolute;
  bottom: 0;
  left: 25%;
}

.album-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.album-card {
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
  background: #ffffff; /* White background */
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  position: relative;
  padding: 20px;
}

.album-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.15);
}

.album-id {
  background: #4caf50; /* Green background for album ID */
  color: white;
  font-weight: bold;
  padding: 10px;
  position: absolute;
  top: 10px;
  left: 10px;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);
}

.album-title {
  font-family: 'Arial', sans-serif;
  font-size: 18px;
  color: #333;
  margin-top: 60px;
  text-align: left;
}

.no-albums {
  margin-top: 30px;
  color: #555;
  font-size: 1.2em;
}
</style>
