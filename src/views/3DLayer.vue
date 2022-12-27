<template>
  <div class="layer-stack__wrap">
    <div
      class="layer-stack__layer layer-stack__layer1"
      :class="[layerSwitch1 == 1 ? 'layer-stack__layer_hover' : '']"
      @click="clickLayer(1)"
    >
      <div class="icon">
        <img src="../assets/Vector.svg" alt="" v-show="layerSwitch1 == 1" />
      </div>
      <h2>B3</h2>
    </div>
    <!-- :class="[layerSwitch1 == 2 ? 'layer-stack__layer_hover' : '']" -->
    <div
      class="layer-stack__layer layer-stack__layer2"
      :class="[layerSwitch1 == 2 ? 'layer-stack__layer_hover' : '']"
      @click="clickLayer(2)"
    >
      <div class="icon">
        <img src="../assets/Vector.svg" alt="" v-show="layerSwitch1 == 2" />
      </div>
      <h2>B2</h2>
    </div>
    <!-- :class="[layerSwitch1 == 3 ? 'layer-stack__layer_hover' : '']" -->
    <div
      class="layer-stack__layer layer-stack__layer3"
      :class="[layerSwitch1 == 3 ? 'layer-stack__layer_hover' : '']"
      @click="clickLayer(3)"
    >
      <!-- <div class="B1_img"></div> -->
      <div class="icon">
        <img src="../assets/Vector.svg" alt="" v-show="layerSwitch1 == 3" />
      </div>
      <h2>B1</h2>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "3D Layer",
  setup() {
    let layerSwitch1 = ref(0);

    const clickLayer = (event) => {
      if (layerSwitch1.value == event) {
        layerSwitch1.value = 0;
      } else {
        layerSwitch1.value = event;
      }
    };

    return { clickLayer, layerSwitch1 };
  },
};
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  outline: none;
  box-sizing: border-box;
}

body {
  background: #b4e0e1;
}

.layer-stack__wrap {
  position: relative;
  margin-top: 27%;
  margin-left: 45%;
}

.layer-stack__layer {
  height: 229.08px;
  width: 428.23px;
  position: absolute;
  transform: rotateX(50deg) rotateZ(30deg) translateZ(0);
  // box-shadow: 0px 0px 10px 2px rgba(0, 0, 0, 0.15);
  transition: all 0.3s ease-out;
  text-align: start;
  display: flex;
  align-items: flex-end;
  cursor: pointer;
  user-select: none;
}

.layer-stack__layer1 {
  background: #e1e2e8; //224687
}
.layer-stack__layer1:hover {
  box-shadow: 1px 1px 10px 2px rgba(0, 0, 0, 0.15);
  transition: (all 0.15s);
}

.layer-stack__layer2 {
  transform: rotateX(50deg) rotateZ(30deg) translateZ(100px);
  background: #ebedf0; //2abfd4
}
.layer-stack__layer2:hover {
  box-shadow: 1px 1px 10px 2px rgba(0, 0, 0, 0.15);
  transition: (all 0.15s);
}

.layer-stack__layer3 {
  transform: rotateX(50deg) rotateZ(30deg) translateZ(200px);
  background: #f8f8f9;
}
.layer-stack__layer3:hover {
  box-shadow: 1px 1px 10px 2px rgba(0, 0, 0, 0.15);
  transition: (all 0.15s);
}

.layer-stack__layer_hover {
  // transform: translateY(-70px) rotateX(0deg) rotateZ(0deg) translateZ(100px)
  //   scale(1.7);
  // z-index: 9;
}

h2 {
  margin: 0 0 15px 5px;
  font-weight: 700;
  display: flex;
  text-align: center;
  align-items: flex-start;
}
.icon {
  width: 30px;
  height: 50px;
  text-align: right;
}

.B1_img {
  width: 100px;
  height: 100px;
  margin: 0 0 0px 40px;
  transform: rotateX(0deg) rotateZ(-13deg);
  background-image: url("../assets/B1.png");
  object-fit: cover;
  background-repeat: no-repeat;
}
</style>
