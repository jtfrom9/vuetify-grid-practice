<template>
  <div class="flex">
    <h3>
      {{ title }}
    </h3>
    <div class="marginleft">
      <slot>
        <span>hoge</span>
      </slot>
    </div>
  </div>
</template>
<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';

@Component
export default class Headline extends Vue {
  @Prop({ type: String, required: true }) readonly title!: string;
}
</script>

<style scoped>
.flex {
  display: flex;
  align-items: center;
}
.marginleft {
  margin-left: 10px;
  flex-grow: 1;
}
</style>
