<template>
  <div>
    <v-container> </v-container>
    <h3>row align -> flexbox align-items</h3>
    <!-- mb-6 = margin bottom -->
    <v-container v-for="align in align_values" :key="align">
      <!-- v-rowは、heightを持っていない。 -->
      <v-row :align="align" no-gutters style="height: 100px">
        <v-col v-for="c in colors" :key="c">
          <!-- v-cardはheightがあるけど、結局styleになるだけ -->
          <v-card :color="c" outlined tile height="30px"> row :align={{ align }} </v-card>
        </v-col>
      </v-row>
    </v-container>

    <h3>col align-self -> flexbox align-self</h3>
    <v-container class="grey lighten-1">
      <v-row no-gutters style="height: 300px">
        <v-col v-for="align in alignself_values" :key="align" :align-self="align">
          <!-- <v-card class="pa-2" outlined tile> {{ align }} </v-card> -->
          <v-card class="pa-2" outlined tile>
            {{ align }}
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <Headline title="flexbox">
      <v-container fluid>
        <v-row align="center">
          <v-col cols="2" class="pa-0">
            <v-slider
              label="inner width"
              v-model="inner_width"
              hide-details
              max="800"
              min="100"
              step="10"
              thumb-label
            ></v-slider>
          </v-col>
          <v-col cols="2" class="pa-0">
            <v-select
              label="justify-content"
              v-model="outer_justify"
              :items="outer_justify_values"
              hide-details
            ></v-select>
          </v-col>
          <v-col cols="2" class="pa-0">
            <v-select label="align-items" v-model="outer_align" :items="outer_align_values" hide-details></v-select>
          </v-col>
          <v-col cols="2" class="pa-0">
            <v-select
              label="align-self(3rd)"
              v-model="inner3_align_self"
              :items="inner3_align_self_values"
              hide-details
            ></v-select>
          </v-col>
        </v-row>
      </v-container>
    </Headline>
    <v-container class="container-background">
      <div
        class="outer"
        :style="{ display: 'flex', height: '300px', justifyContent: outer_justify, alignItems: outer_align }"
      >
        <div class="inner" :style="{ width: `${inner_width}px` }">
          We the People of the United States, in Order to form a more perfect Union, establish Justice, insure domestic
          Tranquility, provide for the common defense, promote the general Welfare, and secure the Blessings of Liberty
          to ourselves and our Posterity, do ordain and establish this Constitution for the United States of America.
        </div>
        <div class="inner" :style="{ width: `${inner_width}px` }">
          We the People of the United States, in Order to form a more perfect Union, establish Justice, insure domestic
          Tranquility, provide for the common defense, promote the general Welfare, and secure the Blessings of Liberty
          to ourselves and our Posterity, do ordain and establish this Constitution for the United States of America.
        </div>
        <div class="inner" :style="{ width: `${inner_width}px`, alignSelf: inner3_align_self }">
          We the People of the United States, in Order to form a more perfect Union, establish Justice, insure domestic
          Tranquility, provide for the common defense, promote the general Welfare, and secure the Blessings of Liberty
          to ourselves and our Posterity, do ordain and establish this Constitution for the United States of America.
        </div>
      </div>
      <!-- </div> -->
    </v-container>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import Headline from './Headline.vue';

type JustifyContentValues = 'flex-start' | 'flex-end' | 'center' | 'space-between' | 'space-around';
type AlignItemValues = 'stretch' | 'flex-start' | 'flex-end' | 'center' | 'baseline';
type AlignSelfValues = 'auto' | AlignItemValues;

@Component({ components: { Headline } })
export default class GridPractice extends Vue {
  private align_values = ['start', 'center', 'end', 'baseline', 'stretch'];
  private alignself_values = ['start', 'center', 'end', 'auto', 'baseline', 'stretch'];
  private colors = ['red', 'blue', 'green'];

  private inner_width = 300;
  private outer_justify_values: JustifyContentValues[] = [
    'center',
    'flex-start',
    'flex-end',
    'space-between',
    'space-around',
  ];
  private outer_justify: JustifyContentValues = 'center';
  private outer_align_values: AlignItemValues[] = ['stretch', 'flex-start', 'flex-end', 'center', 'baseline'];
  private outer_align = 'center';

  private inner3_align_self_values: AlignSelfValues[] = [
    'stretch',
    'flex-start',
    'flex-end',
    'center',
    'baseline',
    'auto',
  ];
  private inner3_align_self = 'auto';
}
</script>

<style scoped>
.container-background {
  padding: 10px;
  background: #e6ecf2;
  margin: 0 auto;
}
.inner {
  background: rgba(255, 255, 255, 0.3);
  border: 1px solid #fff;
}
</style>
