<template>
  <div id="app" class="container">
    <h1 class="title">Daftar Barang</h1>
    <input type="text" v-model="newActivity.name" placeholder="Tambahkan barang baru" class="input">
    <div class="datetime-container">
      <label for="datetime" class="label">Tanggal & Jam:</label>
      <input id="datetime" type="datetime-local" v-model="newActivity.dateTime" class="input">
    </div>
    <button @click="addActivity" class="button">Tambah</button>
    <table class="table">
      <thead>
        <tr>
          <th>Barang</th>
          <th>Tanggal & Jam</th>
          <th>Status</th>
          <th>Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(activity, index) in activities" :key="index">
          <td>{{ activity.name }}</td>
          <td>{{ formatDate(activity.dateTime) }}</td>
          <td>
            <input type="checkbox" v-model="activity.completed" class="checkbox">
            <span :class="{ 'completed': activity.completed }">{{ activity.completed ? 'Selesai' : 'Belum Selesai' }}</span>
          </td>
          <td><button @click="removeActivity(index)" class="button">Hapus</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: {
        name: '',
        dateTime: '',
        completed: false
      },
      activities: []
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity.name && this.newActivity.dateTime) {
        this.activities.push({...this.newActivity});
        this.newActivity.name = '';
        this.newActivity.dateTime = '';
        this.newActivity.completed = false;
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    },
    formatDate(dateTime) {
      if (!dateTime) return '';
      const options = { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' };
      return new Date(dateTime).toLocaleDateString(undefined, options);
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #eaf5e1;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(222, 220, 220, 0.1);
}

.title {
  font-size: 36px;
  font-weight: bold;
  color: #f1f5f1; 
  margin-bottom: 20px;
  text-align: center;
}

.input {
  width: calc(100% - 20px);
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #43853d;
  border-radius: 5px;
  font-size: 16px;
}

.label {
  display: block;
  font-size: 18px;
  margin-bottom: 5px;
  color: #43853d; 
}

.button {
  padding: 10px 20px;
  background-color: #43853d; 
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.button:hover {
  background-color: #347031; 
}

.table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
  background-color: #eaf5e1;

}

.table th,
.table td {
  border: 1px solid #43853d; 
  padding: 10px;
  text-align: center;
}

.checkbox {
  margin: 0;
}

.completed {
  text-decoration: line-through;
}
</style>
