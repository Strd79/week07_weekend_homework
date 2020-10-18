<template>
  <div v-if="selectedSeasons.length > 0" id="seasons">
    <h2>{{ queen.name }} appeared in the following season(s):</h2>
      <ul>
        <li v-for="(season, index) in selectedSeasons" :key="index">
          <h3>Season {{ season.seasonNumber }}</h3>
          <img class="season-pic" :src="season.image_url" alt="Image of season queens">
          <!-- <p>Placed {{ findPlacement(season, queen) }} </p> -->
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'season-details',
  props: ['queen', 'selectedSeasons'],
  methods: {
    findPlacement: function(currentSeason, currentQueen) {
      for (queen in currentSeason.queens) {
        if (queen.id === currentQueen.id) {
          const placement = queen.place
          if (placement === 1) {
            return `${placement}st`
          }
          else if (placement === 2) {
            return `${placement}nd`
          }
          else if (placement === 3) {
            return `${placement}rd`
          }
          else {
            return `${placement}th`
          }
        }
      }
    }
  }
}
</script>

<style>
li {
  list-style: none;
}

.season-pic {
  height: 200px;
}

</style>