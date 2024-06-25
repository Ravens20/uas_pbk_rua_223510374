<template>
  <div id="app" class="container mt-5">
    <h1 class="text-center mb-4">Welcome To Post Todos RUA </h1> 
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Tambah Aktivitas Baru</h5>
        <div class="form-group">
          <label for="activityName">Nama Aktivitas</label>
          <input v-model="newActivity.name" type="text" class="form-control" id="activityName" placeholder="Masukkan nama aktivitas">
        </div>
        <div class="form-group">
          <label for="dateTime">Waktu Aktivitas</label>
          <input v-model="newActivity.dateTime" type="datetime-local" class="form-control" id="dateTime">
        </div>
        <button @click="addActivity" class="btn btn-primary mt-3">Tambahkan Aktivitas</button>
      </div>
    </div>
    <div class="mt-4">
      <h2>Daftar Aktivitas</h2>
      <ul class="list-group">
        <li v-for="(activity, index) in activities" :key="index" class="list-group-item d-flex justify-content-between align-items-center">
          <div>
            <span :class="{ completed: activity.completed }">{{ activity.name }}</span>
            <br>
            <small class="text-muted">{{ formatDate(activity.dateTime) }}</small>
          </div>
          <button @click="removeActivity(index)" class="btn btn-danger btn-sm">Hapus</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: {
        name: '',
        dateTime: ''
      },
      activities: []
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity.name.trim() !== '' && this.newActivity.dateTime.trim() !== '') {
        this.activities.push({ 
          name: this.newActivity.name, 
          dateTime: this.newActivity.dateTime, 
          completed: false 
        });
        this.newActivity.name = '';
        this.newActivity.dateTime = '';
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    },
    formatDate(dateTime) {
      const options = { year: 'numeric', month: 'short', day: 'numeric', hour: 'numeric', minute: 'numeric' };
      return new Date(dateTime).toLocaleDateString('en-US', options);
    }
  }
};
</script>

<style>
body {
  background-color: #f8f9fa;
}

.completed {
  text-decoration: line-through;
}

.card {
  margin-bottom: 20px;
}

.card-title {
  font-weight: bold;
}

.list-group-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.text-muted {
  font-size: 0.9em;
}
</style>
