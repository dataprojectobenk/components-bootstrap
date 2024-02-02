<template>
    <div id="data-table">
        <!-- search and list show -->
        <div class="d-flex justify-content-md-between flex-column flex-md-row align-content-sm-center">
            <div class="list-show  row justify-content-center justify-content-md-start col-12 col-md-8 ">
                <label for="list" class="col-form-label col-auto" :class="prop.size=='sm'?'col-form-label-sm':''">Tampilkan</label>
                <div class="col-auto">
                    <select class="form-select" :class="prop.size=='sm'?'form-select-sm':''" v-model="config.perPage" @change="()=>config.page=1">
                        <option v-for="item in [10, 15, 20, 25, 30]" :value="item">{{ item }}</option>
                    </select>
                </div>
            </div>
            <div class="input-group col mt-1 mt-md-0 " :class="prop.size=='sm'?'input-group-sm':''">
                <input type="text" class="form-control" :class="prop.size=='sm'?'form-control-sm':''" placeholder="Cari..." v-model="config.search">
                <span class="input-group-text"><i class="bi bi-search"></i></span>
            </div>
        </div>
        <!-- end search and list show -->
        <!-- table -->
        <table id="table" class="table mt-2" :class="prop.size=='sm'?prop.classTable+' table-sm':prop.classTable">
            <thead>
                <tr class="align-middle">
                    <th v-for="item in prop.column">{{ item.name }}</th>
                </tr>
            </thead>
            <tbody>
                <tr class="align-middle" v-for="item in dataTable.data">
                    <td v-for="i in  prop.column">{{ item[i.data] }}</td>
                </tr>
            </tbody>
        </table>
        <!-- end table -->
        <div class="justify-content-ceconfig.value.page-1nter d-flex flex-column-reverse flex-md-row justify-content-md-between align-content-center">
            <div class="info text-center " :class="prop.size=='sm'?'small':''">
                hello
            </div>
            <div class="navigation">
                <!-- pagination -->
                    <nav>
                        <ul class="pagination justify-content-center justify-content-md-end" :class="prop.size=='sm'?'pagination-sm':''">
                            <li class="page-item">
                                <button class="page-link"  aria-label="Previous" @click="()=>{config.page=config.page!=1?config.page-1:1}">
                                    <span aria-hidden="true">&laquo;</span>
                                </button>
                            </li>
                            <li class="page-item" v-for="i in Math.ceil(dataTable.length/config.perPage)">
                                <button class="page-link" :class="config.page==i?'active':''" @click="()=>config.page=i">{{ i }}</button>
                            </li>
                            <li class="page-item">
                                <a class="page-link" href="#" aria-label="Next" @click="()=>{config.page=config.page!=Math.ceil(dataTable.length/config.perPage)?config.page+1:Math.ceil(dataTable.length/config.perPage)}">
                                    <span aria-hidden="true">&raquo;</span>
                                </a>
                            </li>
                        </ul>
                    </nav>
                    <!-- end pagination -->
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed , ref} from 'vue';
const config=ref({
    perPage:10,
    page:1,
    search:''
})
const prop = defineProps({
    classTable: String,
    column: {
        default: [],
        type: Array
    },
    data: {
        default: [],
        type: Array
    },
    size:{
        default:'md',
        type:String
    }
})

const dataTable = computed(()=>{
    let dt ={
        length:prop.data.length,
        filter:0,
        data:prop.data
    }

    // show data per page
    let start = 0+ (config.value.page-1)* config.value.perPage
    let end = config.value.page * config.value.perPage
    dt.data = dt.data.slice(start,end)
    return dt
})

</script>

<style lang="scss" scoped>
// #data-table{
// }
</style>