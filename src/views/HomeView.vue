<template>
  <BaseLayout>
    <Datatable class-table="table-striped  table-bordered table-hover" :column="column" :data="users"  :selected="true" ></Datatable>
  </BaseLayout>
</template>

<script setup>
import BaseLayout from '@/components/BaseLayout.vue';
import Datatable from "../components/Datatables/Datatable.vue";
import axios from 'axios'
import { ref,onMounted } from 'vue';

const url = import.meta.env.VITE_API_URL
const users= ref([])

const column = [
  { name: 'Nama depan', data: 'first_name' },
  { name: 'Nama belakang', data: 'last_name' },
  { name: 'Email', data: 'email' },
  { name: 'Jenis kelamin', data: 'gender' },
]

const getUser=async()=>{
  await axios({
    method:'get',
    url:url+'users'
  }).then(res=>{
    users.value = res.data
  })
}

onMounted(async()=>{
  await getUser()
})

</script>

<style lang="scss" scoped></style>