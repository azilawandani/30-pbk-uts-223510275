<template>
  <div>
    <h1>ToDo List</h1>
    <input type="text" v-model="inputKegiatan" @keyup.enter="tambahKegiatan" placeholder="Tambah kegiatan...">
    <input type="checkbox" v-model="filterSelesai"> Tampilkan yang Belum Selesai
    <div v-for="kegiatan in filteredKegiatanList" :key="kegiatan.id">
      <kegiatan :kegiatan="kegiatan" @batalkan="batalkan"></kegiatan>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import Kegiatan from './components/Kegiatan.vue';

export default {
  components: {
    Kegiatan
  },
  setup() {
    const kegiatanList = ref([]);
    const inputKegiatan = ref('');
    const filterSelesai = ref(false);

    const tambahKegiatan = () => {
      if (inputKegiatan.value.trim() !== '') {
        kegiatanList.value.push({
          id: kegiatanList.value.length + 1,
          nama: inputKegiatan.value.trim(),
          selesai: false
        });
        inputKegiatan.value = '';
      }
    };

    const batalkan = (id) => {
      kegiatanList.value = kegiatanList.value.filter(kegiatan => kegiatan.id !== id);
    };

    const filteredKegiatanList = computed(() => {
      return kegiatanList.value.filter(kegiatan => !filterSelesai.value || !kegiatan.selesai);
    });

    return {
      kegiatanList,
      inputKegiatan,
      filterSelesai,
      tambahKegiatan,
      batalkan,
      filteredKegiatanList
    };
  }
}
</script>

<style>
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
