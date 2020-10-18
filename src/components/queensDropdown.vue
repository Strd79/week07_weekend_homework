<template>
  <div>
      <h2>Let's take a look at the Queens</h2>
      <select v-on:change="handleSelection" v-model="selectedQueen">
          <option value="" disabled selected>Pick a queen...</option>
          <option v-for="queen in queens" :value="queen">{{ queen.name }}</option>
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