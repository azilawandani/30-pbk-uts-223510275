<template>
  <div>
    <h1>ToDo List</h1>
    <input type="text" v-model="inputKegiatan" @keyup.enter="tambahKegiatan" placeholder="Tambah kegiatan...">
    <input type="checkbox" v-model="filterSelesai"> Tampilkan yang Belum Selesai
    <div v-for="kegiatan in filteredKegiatanList" :key="kegiatan.id">
      <div class="kegiatan" :class="{ 'selesai': kegiatan.selesai, 'editing': editId === kegiatan.id }">
        <input type="checkbox" v-model="kegiatan.selesai">
        <span v-if="editId !== kegiatan.id">{{ kegiatan.nama }}</span>
        <input type="text" v-model="editedKegiatanNama" ref="editedKegiatanNamaInput" :hidden="editId !== kegiatan.id">
        <button @click="editKegiatan(kegiatan.id)" :disabled="editId === kegiatan.id">Edit</button>
        <button @click="simpanEditKegiatan(kegiatan.id)" :disabled="editId !== kegiatan.id">Simpan</button>
        <button @click="batalkan(kegiatan.id)" :disabled="editId === kegiatan.id">Batal</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const kegiatanList = ref([]);
    const inputKegiatan = ref('');
    const filterSelesai = ref(false);
    const editId = ref(null);
    const editedKegiatanNama = ref('');

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

    const editKegiatan = (id) => {
      editId.value = id;
      const kegiatan = kegiatanList.value.find(kegiatan => kegiatan.id === id);
      if (kegiatan) {
        editedKegiatanNama.value = kegiatan.nama;
      } else {
        console.error('Kegiatan not found with id:', id);
      }
    };

    const simpanEditKegiatan = (id) => {
      const index = kegiatanList.value.findIndex(kegiatan => kegiatan.id === id);
      if (index !== -1) {
        kegiatanList.value[index].nama = editedKegiatanNama.value;
        editId.value = null; 
      }
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
      filteredKegiatanList,
      editId,
      editedKegiatanNama,
      editKegiatan,
      simpanEditKegiatan
    };
  }
};
</script>

<style scoped>
.kegiatan {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

.kegiatan.selesai {
  text-decoration: line-through;
}

.kegiatan.editing {
  background-color: #f0f0f0;
}
</style>
