<template>
    <div id="data-table">
        <!-- search and list show -->
        <div class="d-flex justify-content-md-between flex-column flex-md-row align-content-sm-center">
            <div class="list-show  row justify-content-center justify-content-md-start col-12 col-md-8 ">
                <label for="list" class="col-form-label col-auto" :class="prop.size=='sm'?'col-form-label-sm':''">Tampilkan</label>
                <div class="col-auto">
                    <select class="form-select" :class="prop.size=='sm'?'form-select-sm':''">
                        <option v-for="item in [10, 15, 20, 25, 30]" :value="item">{{ item }}</option>
                    </select>
                </div>
            </div>
            <div class="input-group col mt-1 mt-md-0 " :class="prop.size=='sm'?'input-group-sm':''">
                <input type="text" class="form-control" :class="prop.size=='sm'?'form-control-sm':''" placeholder="Cari...">
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
                <tr class="align-middle" v-for="item in prop.data">
                    <td v-for="i in  prop.column">{{ item[i.data] }}</td>
                </tr>
            </tbody>
        </table>
        <!-- end table -->
        <div class="justify-content-center d-flex flex-column-reverse flex-md-row justify-content-md-between align-content-center">
            <div class="info text-center " :class="prop.size=='sm'?'small':''">
                hello
            </div>
            <div class="navigation">
                <!-- pagination -->
                    <nav>
                        <ul class="pagination justify-content-center justify-content-md-end" :class="prop.size=='sm'?'pagination-sm':''">
                            <li class="page-item">
                                <a class="page-link" href="#" aria-label="Previous">
                                    <span aria-hidden="true">&laquo;</span>
                                </a>
                            </li>
                            <li class="page-item"><a class="page-link" href="#">1</a></li>
                            <li class="page-item"><a class="page-link" href="#">2</a></li>
                            <li class="page-item"><a class="page-link" href="#">3</a></li>
                            <li class="page-item">
                                <a class="page-link" href="#" aria-label="Next">
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
</script>

<style lang="scss" scoped>
// #data-table{
// }
</style>