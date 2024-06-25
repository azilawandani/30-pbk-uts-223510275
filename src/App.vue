<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title>
          My Project
        </q-toolbar-title>

        <q-btn flat label="Todos" @click="navigateTo('/todos')" />
        <q-btn flat label="Posts" @click="navigateTo('/posts')" />
        <q-btn flat label="Albums" @click="navigateTo('/albums')" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  methods: {
    navigateTo(route) {
      this.$router.push(route)
    }
  }
}

</script>

<style>
header {
  background-color: #98b0c9;
  padding: 10px;
}

nav ul {
  list-style-type: none;
  padding: 0;
}

nav li {
  display: inline;
  margin-right: 20px;
}

nav li a {
  color: white;
  text-decoration: none;
  font-size: 18px;
}

nav li:hover {
  background-color: #46568b;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #7fa0c1;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
  color: #333;
  text-align: center;
}

input[type="text"] {
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 8px;
  margin-bottom: 8px;
}

button {
  padding: 8px 16px;
  font-size: 16px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 8px;
}

button:hover {
  background-color: #0056b3;
}

.kegiatan {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 8px;
  padding: 8px;
  background-color: #f1f1f1;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.kegiatan.selesai {
  text-decoration: line-through;
  color: #777;
}

.checkbox-label {
  margin-right: 8px;
}

.checkbox-label input {
  margin-right: 4px;
  cursor: pointer;
}

.checkbox-label span {
  cursor: pointer;
}

.button-container {
  margin-left: auto;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

.fade-in {
  animation: fadeIn 0.5s ease;
}

button.delete-button {
  background-color: #dc3545;
}

button.delete-button:hover {
  background-color: #c82333;
}

input[type="checkbox"] {
  margin-right: 8px;
  cursor: pointer;
}

input[type="checkbox"]:checked + span {
  color: #777;
  text-decoration: line-through;
}
</style>
