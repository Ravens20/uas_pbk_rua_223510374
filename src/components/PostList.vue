<template>
  <div class="post-list">
    <h1>POST</h1>
    <div class="user-selection">
      <label for="users">Pilih User:</label>
      <select id="users" v-model="selectedUserId" @change="loadUserPosts">
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
    </div>
    <div class="user-posts">
      <div v-if="loading" class="loading">Loading...</div>
      <div v-else>
        <div v-for="post in userPosts" :key="post.id" class="post">
          <h2>{{ post.title }}</h2>
          <p>{{ post.body }}</p>
        </div>
        <div v-if="userPosts.length === 0" class="no-posts">
          No posts found for this user.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PostList',
  data() {
    return {
      users: [],
      selectedUserId: null,
      userPosts: [],
      loading: false
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(data => {
          this.users = data;
        })
        .catch(error => {
          console.error('Error fetching users:', error);
        });
    },
    loadUserPosts() {
      if (!this.selectedUserId) return;
      this.loading = true;
      fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUserId}`)
        .then(response => response.json())
        .then(data => {
          this.userPosts = data;
          this.loading = false;
        })
        .catch(error => {
          console.error('Error fetching user posts:', error);
          this.loading = false;
        });
    }
  }
};
</script>

<style scoped>
.post-list {
  background-color: #eaf5e1; 
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 800px;
  margin: 50px auto;
}

.post-list h1 {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #43853d; 
  text-align: center;
  font-size: 36px;
  margin-bottom: 20px;
}

.user-selection {
  margin-bottom: 20px;
}

.user-selection label {
  font-size: 18px;
  margin-right: 10px;
  color: #43853d;
}

.user-selection select {
  font-size: 16px;
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #43853d; 
  background-color: #d8f3dc; 
  color: #43853d; 
  width: 200px;
}

.user-posts {
  margin-top: 20px;
}

.loading {
  font-size: 18px;
  color: #43853d; 
  margin-top: 20px;
}

.post {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
  text-align: left;
}

.post h2 {
  color: #43853d; 
  font-size: 24px;
  margin-bottom: 10px;
}

.post p {
  color: #666;
  font-size: 16px;
}

.no-posts {
  color: #43853d; 
  margin-top: 20px;
}
</style>
