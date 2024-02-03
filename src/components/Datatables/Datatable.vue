<template>
    <div id="data-table">
        <!-- search and list show -->
        <div class="d-flex justify-content-md-between flex-column flex-md-row align-content-sm-center">
            <div class="list-show  row justify-content-center justify-content-md-start col-12 col-md-8 ">
                <label for="list" class="col-form-label col-auto"
                    :class="prop.size == 'sm' ? 'col-form-label-sm' : ''">Tampilkan</label>
                <div class="col-auto">
                    <select class="form-select" :class="prop.size == 'sm' ? 'form-select-sm' : ''" v-model="config.perPage"
                        @change="() => config.page = 1">
                        <option v-for="item in [10, 15, 20, 25, 30]" :value="item">{{ item }}</option>
                    </select>
                </div>
            </div>
            <div class="input-group col mt-1 mt-md-0 " :class="prop.size == 'sm' ? 'input-group-sm' : ''">
                <input type="text" class="form-control" :class="prop.size == 'sm' ? 'form-control-sm' : ''"
                    placeholder="Cari..." v-model="config.search" @keyup="() => config.page = 1">
                <span class="input-group-text"><i class="bi bi-search"></i></span>
            </div>
        </div>
        <!-- end search and list show -->
        <!-- table -->
        <table id="table" class="table mt-2" :class="prop.size == 'sm' ? prop.classTable + ' table-sm' : prop.classTable">
            <thead>
                <tr class="align-middle">
                    <th v-if="prop.selected"><input type="checkbox" v-model="selectAll"></th>
                    <th v-for="item in prop.column">{{ item.name }}</th>
                </tr>
            </thead>
            <tbody>
                <tr class="align-middle " v-for="item in dataTable.data" @click="emits('onEdit', item.id)">
                    <td v-if="prop.selected">
                        <input type="checkbox" :value="item.id" v-model="selected" @change="emits('onSelected', selected)">
                    </td>
                    <td v-for="i in  prop.column">{{ item[i.data] }}</td>
                </tr>
            </tbody>
        </table>
        <!-- end table -->
        <div
            class="justify-content-ceconfig.value.page-1nter d-flex flex-column-reverse flex-md-row justify-content-md-between align-content-center">
            <div class="info text-center " :class="prop.size == 'sm' ? 'small' : ''">
                <span class="text-mute">Menampilkan {{ dataTable.filter }} dari {{ prop.data.length }}</span>
            </div>
            <div class="navigation">
                <!-- pagination -->
                <nav>
                    <ul class="pagination justify-content-center justify-content-md-end"
                        :class="prop.size == 'sm' ? 'pagination-sm' : ''">
                        <li class="page-item">
                            <button class="page-link" aria-label="Previous"
                                @click="() => { config.page = config.page != 1 ? config.page - 1 : 1 }">
                                <span aria-hidden="true">&laquo;</span>
                            </button>
                        </li>
                        <li class="page-item" v-for="i in Math.ceil(dataTable.filter / config.perPage)">
                            <button class="page-link" :class="config.page == i ? 'active' : ''"
                                @click="() => config.page = i">{{ i
                                }}</button>
                        </li>
                        <li class="page-item">
                            <a class="page-link" href="#" aria-label="Next"
                                @click="() => { config.page = config.page != Math.ceil(dataTable.filter / config.perPage) ? config.page + 1 : Math.ceil(dataTable.length / config.perPage) }">
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
import { computed, ref, watch } from 'vue';
const selected = ref([])
const selectAll = ref(false)
const config = ref({
    perPage: 10,
    page: 1,
    search: ''
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
    size: {
        default: 'md',
        type: String
    },
    filter: {
        default: [],
        type: Array
    },
    selected: {
        default: false,
        type: Boolean
    }
})

const emits = defineEmits(['onSelected', 'onEdit','onSelectAll'])

const dataTable = computed(() => {
    let dt = {
        length: prop.data.length,
        filter: prop.data.length,
        data: prop.data
    }
    // filter data
    if (config.value.search.length > 0) {
        let filter = []
        if (prop.filter.length > 0) {
            filter = prop.filter
        } else {
            prop.column.forEach(el => { filter.push(el.data) })
        }

        // filter data by search
        dt.data = dt.data.filter(el => {
            let isExists = false
            filter.forEach(item => {
                if (el[item].toUpperCase().includes(config.value.search.toUpperCase())) {
                    isExists = true
                    return
                }
            })
            if (isExists) return el
        })
        dt.filter = dt.data.length
    }
    // show data per page
    let start = 0 + (config.value.page - 1) * config.value.perPage
    let end = config.value.page * config.value.perPage
    dt.data = dt.data.slice(start, end)
    return dt
})

watch(selectAll, () => {
    if (selectAll.value) {
        selected.value = []
        document.querySelectorAll('#data-table #table tbody input[type="checkbox"]').forEach(el => {
            selected.value.push(el.value)
        })
    } else {
        selected.value = []
    }
    emits('onSelectAll',selected.value)
})
</script>

<style lang="scss" scoped>
#data-table {
    tbody tr td {
        cursor: pointer;
    }
}
</style>