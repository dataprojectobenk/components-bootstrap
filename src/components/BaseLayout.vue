<template>
    <nav class="navbar navbar-light shadow-sm navbar-expand">
        <div class="container">
            <span class="navbar-brand fw-bold">Kumpulan Component</span>
            <div class="navbar-collapse">
                <ul class="navbar-nav mb-2 mb-lg-0">
                    <li class="nav-item">
                        <RouterLink to="/" class="nav-link">Datatable</RouterLink>
                    </li>
                    <li class="nav-item">
                        <RouterLink to="/dashboardv1" class="nav-link">DashboardV1</RouterLink>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
    <div class="container mt-3">
        <slot></slot>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped></style>