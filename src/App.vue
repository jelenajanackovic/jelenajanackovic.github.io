<template>
  <div class="bg-secondary bg-gradient">
  <nav class="navbar navbar-expand-lg navbar-light  bg-secondary bg-gradient">
    <div class="container-fluid">
      <a class="navbar-brand" href="#"><img src="@/assets/airserbia.png" height="24"></a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">About</router-link>
          </li>

        </ul>
      </div>
    </div>
  </nav>
  <div class="container bg-secondary bg-gradient">
    <router-view />
  </div>
  <footer class="text-center bg-secondary bg-gradient">
    &copy; {{ year }} Univerzitet Singidunum
  </footer>
</div>
</template>


<script setup>
const year = new Date().getFullYear();
</script>

<style>


</style>