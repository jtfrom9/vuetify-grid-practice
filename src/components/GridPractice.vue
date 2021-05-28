<template>
  <div>
    <Headline title="v-row justify">
      <v-container fluid>
        <v-row align="center">
          <v-col cols="2" class="pa-0">
            <v-checkbox label="fluid" v-model="fluid" hide-details class="ma-0"></v-checkbox>
          </v-col>
          <v-col cols="2" class="pa-0">
            <v-select
              :items="valign_item_values"
              label="v-row align"
              v-model="row_test_row_align"
              hide-details
            ></v-select>
          </v-col>
          <v-col cols="3" class="pa-0">
            <v-slider
              label="row height"
              v-model="row_test_row_height"
              hide-details
              max="300"
              min="10"
              step="10"
              thumb-label
            ></v-slider>
          </v-col>
        </v-row>
      </v-container>
    </Headline>
    <v-container :fluid="fluid" class="container-background">
      <v-row v-for="justify in vjustify_values" :key="justify">
        <v-col cols="2" class="inner" align-self="center">
          {{ justify }}
        </v-col>
        <v-col :style="{ height: `${row_test_row_height}px` }" class="pa-0 d-flex">
          <v-container fluid class="d-flex">
            <v-row :justify="justify" class="flex-grow-1" :align="row_test_row_align">
              <v-col cols="1" class="pa-0 d-flex">
                <v-card class="flex-grow-1 text-center"> cols=1 </v-card>
              </v-col>
              <v-col cols="2" class="pa-0 d-flex">
                <v-card class="flex-grow-1 text-center"> cols=2 </v-card>
              </v-col>
              <v-col cols="3" class="pa-0 d-flex">
                <v-card class="flex-grow-1 text-center"> cols=3 </v-card>
              </v-col>
              <v-col cols="4" class="pa-0 d-flex">
                <v-card class="flex-grow-1 text-center"> cols=4 </v-card>
              </v-col>
            </v-row>
          </v-container>
        </v-col>
      </v-row>

      <!--
        <v-row
        v-for="align in valign_item_values"
        :key="align"
        :align="align"
        no-gutters
        style="height: 100px"
      >
        <v-col v-for="c in colors" :key="c">
          <v-card :color="c" outlined tile height="30px"> row :align={{ align }} </v-card>
        </v-col>
      </v-row>
      -->
    </v-container>

    <Headline title="v-col align-self">
      <v-container fluid>
        <v-row align="center">
          <v-col cols="2" class="pa-0">
            <v-select
              :items="valign_item_values"
              label="v-row align"
              v-model="col_test_row_align"
              hide-details
            ></v-select>
          </v-col>
          <v-col cols="3" class="pa-0">
            <v-slider
              label="row height"
              v-model="col_test_row_height"
              hide-details
              max="600"
              min="10"
              step="10"
              thumb-label
            ></v-slider>
          </v-col>
        </v-row>
      </v-container>
    </Headline>
    <v-container :fluid="fluid" class="container-background">
      <v-row no-gutters :style="{ height: `${col_test_row_height}px` }" :align="col_test_row_align">
        <v-col v-for="align in valign_self_values" :key="align" :align-self="align" class="inner d-flex align-stretch">
          <v-card class="flex-grow-1" :style="{ textAlign: 'center' }">
            v-col align={{ align }} ( We the People of the United States, in Order to form a more perfect Union,
            establish Justice, insure domestic )</v-card
          >
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
              :items="flex_justify_values"
              hide-details
            ></v-select>
          </v-col>
          <v-col cols="2" class="pa-0">
            <v-select label="align-items" v-model="outer_align" :items="flex_align_item_values" hide-details></v-select>
          </v-col>
          <v-col cols="2" class="pa-0">
            <v-select
              label="align-self(3rd)"
              v-model="inner3_align_self"
              :items="flex_align_self_values"
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

type FlexJustifyContentValues = 'flex-start' | 'flex-end' | 'center' | 'space-between' | 'space-around';
type FlexAlignItemValues = 'stretch' | 'flex-start' | 'flex-end' | 'center' | 'baseline';
type FlexAlignSelfValues = 'auto' | FlexAlignItemValues;
type VAlignItemValues = 'stretch' | 'start' | 'end' | 'center' | 'baseline';
type VAlignSelfValues = 'auto' | VAlignItemValues;
type VJustifyValues = 'start' | 'center' | 'end' | 'space-between' | 'space-around';

@Component({ components: { Headline } })
export default class GridPractice extends Vue {
  private flex_justify_values: FlexJustifyContentValues[] = [
    'center',
    'flex-start',
    'flex-end',
    'space-between',
    'space-around',
  ];
  private flex_align_item_values: FlexAlignItemValues[] = ['stretch', 'flex-start', 'flex-end', 'center', 'baseline'];
  private flex_align_self_values: FlexAlignSelfValues[] = [
    'stretch',
    'flex-start',
    'flex-end',
    'center',
    'baseline',
    'auto',
  ];
  private valign_item_values: VAlignItemValues[] = ['stretch', 'start', 'end', 'center', 'baseline'];
  private valign_self_values: VAlignSelfValues[] = ['auto', 'stretch', 'start', 'end', 'center', 'baseline'];
  private vjustify_values: VJustifyValues[] = ['start', 'center', 'end', 'space-between', 'space-around'];

  private fluid = true;
  private colors = ['red', 'blue', 'green'];

  private row_test_row_align = 'center';
  private row_test_row_height = 100;
  private col_test_row_align = 'stretch';
  private col_test_row_height = 300;

  private inner_width = 300;
  private outer_justify: FlexJustifyContentValues = 'center';
  private outer_align = 'center';

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
  background: rgba(255, 255, 255, 0.3) !important;
  border: 1px solid #fff;
}
</style>
