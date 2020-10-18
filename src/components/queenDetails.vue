<template>
  <div v-if="queen">
      <h2>{{ queen.name }}</h2>
        <blockquote>{{ queen.quote }}</blockquote>
        <img class="queen-pic" :src="queen.image_url" :alt="queen.name">
  </div>
</template>

<script>
export default {
    name: 'queen-details',
    props: ['queen', 'seasons'],
}
</script>

<style>
    .queen-pic {
        height: 600px;
    }

</style>