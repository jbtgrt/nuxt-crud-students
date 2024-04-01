<template>
  <div >
    <h1>I am contact us Page</h1>
  </div>
</template>

<script setup lang="ts">
  useHead({
    title: 'Contact Us Page',
  })

  // if (!data.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page Not Found' })
// }
</script>

<style>

</style>