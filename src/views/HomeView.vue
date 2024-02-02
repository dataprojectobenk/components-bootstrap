<template>
  <BaseLayout>
    <Datatable class-table="table-striped  table-bordered" :column="column" :data="dataSiswa" size="sm"></Datatable>
  </BaseLayout>
</template>

<script setup>
import BaseLayout from '@/components/BaseLayout.vue';
import Datatable from "../components/Datatables/Datatable.vue";

const column = [
  { name: 'Nama lengkap', data: 'nama' },
  { name: 'Alamat', data: 'alamat' },
  { name: 'Kelas', data: 'kelas' },
]

const dataSiswa = [
  { id: 1, nama: 'Jono', alamat: 'Citalang', kelas: 10 },
  { id: 2, nama: 'Jono', alamat: 'Citalang', kelas: 10 },
  { id: 3, nama: 'Jono', alamat: 'Citalang', kelas: 10 },
  { id: 4, nama: 'Jono', alamat: 'Citalang', kelas: 10 },
  { id: 5, nama: 'Jono', alamat: 'Citalang', kelas: 10 },
  { id: 6, nama: 'Jono', alamat: 'Citalang', kelas: 10 },
]
</script>

<style lang="scss" scoped></style>