<template>
    <nav class="navbar navbar-light shadow-sm">
        <div class="container">
            <span class="navbar-brand fw-bold">Kumpulan Component</span>
            <ul class="navbar-nav">
                <li class="nav-item">
                    <RouterLink to="/" class="nav-link">Datatable</RouterLink>
                </li>
            </ul>
        </div>
    </nav>
    <div class="container mt-3">
        <slot></slot>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>

</style>