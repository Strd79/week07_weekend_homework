<template>
  <div id="app">
    <header>
      <div>
        <img id="hp-logo" alt="RuPaul's Drag Race logo" src="./assets/drag_race_logo_1280x544.png">
        <h1>Start your engines...!</h1>
      </div>
    </header>
    <main>
      <div>
        <queens-dropdown :queens='queens'></queens-dropdown>
        <queen-details :queen='selectedQueen' :seasons='seasons'></queen-details>
      </div>
      <div>
        <season-details :queen='selectedQueen' :selectedSeasons='selectedSeasons'></season-details>
      </div>
    </main>
  </div>
</template>

<script>
import { eventBus } from './main.js';
import queensDropdown from './components/queensDropdown.vue';
import queenDetails from './components/queenDetails.vue';
import seasonDetails from './components/seasonDetails.vue';

export default {
  name: 'App',
  data() {
    return {
      queens: [],
      seasons: [],
      selectedQueen: null,
      selectedSeasons: [],
    }
  },
  methods: {
    findQueensSeasons: function(queen) {
      const seasons = queen.seasons
      seasons.forEach((season) => {
        fetch(`http://www.nokeynoshade.party/api/seasons/${season.id}`)
        .then(response => response.json())
        .then(season => this.selectedSeasons.push(season))
      })
    }
  },
  mounted() {
    fetch('http://www.nokeynoshade.party/api/queens')
    .then(response => response.json())
    .then(queens => this.queens = queens)

    eventBus.$on('selected-queen', (queen) => {
      this.selectedSeasons = []
      this.selectedQueen = queen;
      this.findQueensSeasons(this.selectedQueen)
    })
  },
  components: {
    'queens-dropdown': queensDropdown,
    'queen-details': queenDetails,
    'season-details': seasonDetails,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#hp-logo {
  width: 250px;
}

</style>
