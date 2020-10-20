<template>
  <div>
      <h2>Let's take a look at the Queens</h2>
      <select v-on:change="handleSelection" v-model="selectedQueen">
          <option value="" disabled selected>Pick a queen...</option>
          <template v-for="queensArray in queens">
          <option v-for="queen in queensArray" :value="queen">{{ queen.name }}</option>
          </template>
      </select>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
    name: 'queens-dropdown',
    props: ['queens'],
    data() {
        return {
            'selectedQueen': {}
        }
    },
    methods: {
        handleSelection() {
            eventBus.$emit('selected-queen', this.selectedQueen)
        }
    },
}
</script>

<style>

</style>