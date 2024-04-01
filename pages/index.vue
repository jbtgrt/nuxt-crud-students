<template>
  <div>
    <h1>I am home Page</h1>

    <button @click="open = true">
      Open Modal
    </button>
    <Teleport to="body">
      <div v-if="open" class="modal">
        <p>Hello from the modal!</p>
        <button @click="open = false">
          Close
        </button>
      </div>
    </Teleport>
  </div>
</template>

<script setup>
  useHead({
    title: 'Home Page',
  })
</script>

<style>

</style>