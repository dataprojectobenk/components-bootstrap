<template>
    <main id="main" class="d-flex">
        <Sidebar />
        <div id="main-content">
            <Navbarv1 />
            <!-- Content web -->
            <div id="content">
                <slot></slot>
            </div>
            <!-- end content web -->
        </div>
    </main>
</template>

<script setup>
import Sidebar from './Sidebar.vue';
import Navbarv1 from '@/components/DashboardV1/Navbarv1.vue'
</script>

<style lang="scss" scoped>
$sidebar : 250px;
$bg-background:rgb(245, 247, 248);
$primary-color : #11009E;
$secondary-color:rgb(252, 103, 54);

  
    main#main{
        background-color: $bg-background;
        #side-bar{
            width: $sidebar;
            background-color: $primary-color;
        }
        #main-content{
            width:calc(100% - $sidebar);
        }   
    }
</style>