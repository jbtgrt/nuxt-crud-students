<template>
  <div>
    <nav class="navbar navbar-expand-lg bg-body-tertiary shadow">
      <div class="container">
        <NuxtLink class="navbar-brand" href="/">NUXT 3 CRUD</NuxtLink>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <NuxtLink class="nav-link active" aria-current="page" href="/">Home</NuxtLink>
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" href="/about-us">About Us</NuxtLink>
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" href="/contact-us">Contact Us</NuxtLink>
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" href="/students">Students</NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script setup>

</script>

<style>

</style>