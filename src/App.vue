<template>
  <v-app>
    <v-main>
      <GridPractice></GridPractice>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

import GridPractice from './components/GridPractice.vue';
@Component({ components: { GridPractice } })
export default class App extends Vue {}
</script>
