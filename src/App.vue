<template>
  <div style="background-color: #f1f6fa">
    <nav class="navbar navbar-expand-lg navbar navbar-light" style="background-color: #f1f6fa">
      <div class="container-fluid">
        <a class="navbar-brand" style="background-color: white;" href="#"><img src="@/assets/airserbia.png" height="24"></a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
          aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link class="nav-link  fw-bold" aria-current="page" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link fw-bold" to="/search">Search</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link fw-bold" to="/about">About</router-link>
            </li>

          </ul>
        </div>
      </div>
    </nav>
    <div class="container" style="background-color: #f1f6fa">
      <router-view />
    </div>
    <footer class="text-center " style="background-color: #f1f6fa">
      &copy; {{ year }} Univerzitet Singidunum
    </footer>
  </div>
</template>


<script setup>
const year = new Date().getFullYear();
</script>

<style></style>