<template>
  <div class="album-details-container" :style="{ backgroundImage: backgroundUrl }">
    <div class="content-wrapper">
      <h2 class="heading">Choose Album:</h2>
      <select v-model="selectedAlbum" @change="fetchPhotos" class="album-select">
        <option v-for="album in albums" :key="album.id" :value="album.id">{{ album.title }}</option>
      </select>
      <h2 class="heading">Photos in Album {{ selectedAlbum }}</h2>
      <table v-if="photos.length" class="photos-table">
        <thead>
          <tr>
            <th>Thumbnail</th>
            <th>Title</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="photo in photos" :key="photo.id">
            <td>
              <img :src="photo.thumbnailUrl" @click="showPhoto(photo.url)" class="thumbnail">
            </td>
            <td>{{ photo.title }}</td>
          </tr>
        </tbody>
      </table>
      <div v-else class="no-photos">
        <p>No photos available.</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const selectedAlbum = ref(route.params.id || '')
const albums = ref([])
const photos = ref([])


const fetchAlbums = async () => {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/albums`)
    albums.value = await response.json()
  } catch (error) {
    console.error('Error fetching albums:', error)
  }
}

const fetchPhotos = async () => {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/albums/${selectedAlbum.value}/photos`)
    photos.value = await response.json()
  } catch (error) {
    console.error('Error fetching photos:', error)
  }
}

const showPhoto = (url) => {
  window.open(url, '_blank')
}

onMounted(() => {
  fetchAlbums()
  if (selectedAlbum.value) {
    fetchPhotos()
  }
})

watch(selectedAlbum, () => {
  if (selectedAlbum.value) {
    fetchPhotos()
  }
})
</script>

<style scoped>
.album-details-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-size: cover;
  background-position: center;
  padding: 20px;
  transition: background-image 0.5s ease-in-out;
}

.content-wrapper {
  background: rgba(255, 255, 255, 0.95);
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 4px 20px rgba(197, 100, 100, 0.1);
  max-width: 800px;
  width: 100%;
  text-align: center;
}

.heading {
  color: #4caf50; 
  margin-bottom: 20px;
}

.album-select {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  font-size: 16px;
  border: 1px solid #4caf50; 
  border-radius: 5px;
  transition: border-color 0.3s;
}

.album-select:hover {
  border-color: #388e3c;
}

.photos-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.photos-table th,
.photos-table td {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: center;
}

.thumbnail {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border: 1px solid #4caf50; 
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.3s, border-color 0.3s;
}

.thumbnail:hover {
  border-color: #388e3c; 
  transform: scale(1.05);
}

.no-photos {
  margin-top: 20px;
  color: #333;
  font-size: 1.2em;
}
</style>
