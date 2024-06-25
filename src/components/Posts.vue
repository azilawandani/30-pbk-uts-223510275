<template>
    <div>
      <h1>Postingan Pengguna</h1>
      <select v-model="selectedUser" @change="fetchPosts">
        <option v-for="user in users" :value="user.id" :key="user.id">{{ user.name }}</option>
      </select>
      <div v-for="post in posts" :key="post.id">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  
  export default {
    setup() {
      const selectedUser = ref(null);
      const users = ref([]);
      const posts = ref([]);
  
      const fetchUsers = async () => {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users');
          const data = await response.json();
          console.log("Users:", data); // Debugging
          users.value = data;
        } catch (error) {
          console.error('Error fetching users:', error);
        }
      };
  
      const fetchPosts = async () => {
        if (!selectedUser.value) return;
        try {
          const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
          const data = await response.json();
          console.log("Posts:", data); // Debugging
          posts.value = data;
        } catch (error) {
          console.error('Error fetching posts:', error);
        }
      };
  
      onMounted(() => {
        fetchUsers(); // Fetch users when component is mounted
      });
  
      return {
        selectedUser,
        users,
        posts,
        fetchPosts
      };
    }
  };
  </script>
  
  <style scoped>
  select {
    padding: 8px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-right: 8px;
    margin-bottom: 8px;
    justify-content: center;
  }

  .posts-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  }
  
  h1 {
    color: #333;
    text-align: center;
  }
  
  h3 {
    color: #555;
  }
  
  p {
    color: #777;
  }
  </style>
  