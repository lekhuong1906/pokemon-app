<template>
  <main-screen v-if="statusMatch == 'default'" @onStart="onHandleBeforeStart($event)"></main-screen>
  <interact-screen v-if="statusMatch == 'match'" :cardsContext="settings.cardsContext">
  </interact-screen>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from './components/InteractScreen.vue';
import { shuffled } from './utils/array.js'

export default {
  name: "App",
  data() {
    return {
      settings: {
        totlalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    }
  },
  components: {
    MainScreen,
    InteractScreen
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totlalOfBlocks = config.totlalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totlalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards]; // es6 copy array
      const cards = [...firstCards, ...secondCards]; //es6 merge array
      this.settings.cardsContext = shuffled(shuffled(shuffled(cards))); //random array
      this.settings.startedAt = new Date().getTime(); //get current time
      this.statusMatch = "match";
    },

  }
}
</script>