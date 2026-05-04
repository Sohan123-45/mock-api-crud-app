<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark shadow sticky-top">
        <div class="container">
            <a class="navbar-brand fw-bold" href="#">
                <i class="bi bi-database-fill me-2"></i>CRUD App
            </a>

            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav w-100 justify-content-around text-center">
                    <li class="nav-item">
                        <a class="nav-link" href="#post">
                            <i class="bi bi-plus-circle me-1"></i>Post
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#get">
                            <i class="bi bi-table me-1"></i>Get
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#update">
                            <i class="bi bi-pencil-square me-1"></i>Update
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link text-danger fw-semibold" href="#delete">
                            <i class="bi bi-trash me-1"></i>Delete
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<script>
export default{
    name:'NavBar'
}
</script>

<style scoped>
    .navbar-brand {
        letter-spacing: 1px;
    }

    .nav-link:hover {
        color: #0d6efd !important;
        transition: 0.3s;
    }
</style>