<template>
  <div id="" class="container">
    <div class="row">
      <parkingLayer />
    </div>
    <div class="row">
      <div class="col">
        <input type="text" v-model="num" />
        <div class="progress vertical">
          <div
            class="progress-bar bg-success"
            role="progressbar"
            :style="'width:' + progressNum + '%'"
            aria-valuenow="90"
            aria-valuemin="0"
            aria-valuemax="100"
          ></div>
        </div>
        <div>width:{{ progressNum }}%</div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import parkingLayer from "../components/parkingLayer.vue";
export default {
  name: "3D Layer",
  components: { parkingLayer },
  setup() {
    let num = ref(10);
    const progressNum = computed(() => {
      return `${num.value}`;
    });

    return { num, progressNum };
  },
};
</script>

<style lang="scss" scoped>
.vertical {
  display: inline-block;
  width: 20%;
  height: 40px;
  -webkit-transform: rotate(-90deg); /* Chrome, Safari, Opera */
  transform: rotate(-90deg);
}
</style>
