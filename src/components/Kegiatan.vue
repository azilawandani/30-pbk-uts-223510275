<template>
    <div class="kegiatan" :class="{ 'selesai': kegiatan.selesai }">
      <input type="checkbox" v-model="kegiatan.selesai">
      <span>{{ kegiatan.nama }}</span>
      <button @click="batalkan(kegiatan.id)">Batal</button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['kegiatan'],
    methods: {
      batalkan(id) {
        this.$emit('batalkan', id);
      }
    }
  }
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
  </style>
  