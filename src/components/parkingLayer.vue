<template>
  <div id="Layer" class="container">
    <div class="layer-stack__wrap">
      <div
        class="layer-stack__layer layer-stack__layer1"
        :class="[layerSwitch1 == 1 ? 'layer-stack__layer_hover' : '']"
        @click="clickLayer(1)"
      >
        <div
          class="arrow-box"
          :class="[layerSwitch == 1 ? 'arrow-right' : '']"
        ></div>
        <h2>B3</h2>
      </div>
      <div
        class="layer-stack__layer layer-stack__layer2"
        :class="[layerSwitch1 == 2 ? 'layer-stack__layer_hover' : '']"
        @click="clickLayer(2)"
      >
        <div
          class="arrow-box"
          :class="[layerSwitch == 2 ? 'arrow-right' : '']"
        ></div>
        <h2>B2</h2>
      </div>
      <div
        class="layer-stack__layer layer-stack__layer3"
        :class="[layerSwitch1 == 3 ? 'layer-stack__layer_hover' : '']"
        @click="clickLayer(3)"
      >
        <div
          class="arrow-box"
          :class="[layerSwitch == 3 ? 'arrow-right' : '']"
        ></div>
        <h2>B1</h2>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "3D Layer",
  setup() {
    let layerSwitch = ref(0);

    const clickLayer = (event) => {
      if (layerSwitch.value == event) {
        layerSwitch.value = 0;
      } else {
        layerSwitch.value = event;
      }
    };

    return { clickLayer, layerSwitch };
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
#Layer {
  width: 600px;
  height: 600px;
}
// body {
//   background: #b4e0e1;
// }

.layer-stack__wrap {
  position: relative;
  margin-top: 27%;
  margin-left: 45%;
}

// 每一層地板
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
  height: 239.08px;
  width: 438.23px;
  box-shadow: 1px 1px 10px 2px rgba(0, 0, 0, 0.275);
  transition: (all 0.15s);
}

// 第二層浮起來
.layer-stack__layer2 {
  transform: rotateX(50deg) rotateZ(30deg) translateZ(100px);
  background: #ebedf0; //2abfd4
}
.layer-stack__layer2:hover {
  height: 239.08px;
  width: 438.23px;
  box-shadow: 1px 1px 10px 2px rgba(0, 0, 0, 0.15);
  transition: (all 0.15s);
}

// 第三層浮起來
.layer-stack__layer3 {
  transform: rotateX(50deg) rotateZ(30deg) translateZ(200px);
  background: #f8f8f9;
}
.layer-stack__layer3:hover {
  height: 239.08px;
  width: 438.23px;
  box-shadow: 1px 1px 10px 2px rgba(0, 0, 0, 0.15);
  transition: (all 0.15s);
}

// .layer-stack__layer:hover {
// transform: translateY(-70px) rotateX(0deg) rotateZ(0deg) translateZ(100px)
//   scale(1.7);
// z-index: 9;
// }

h2 {
  margin: 0 0 15px 0px;
  font-weight: 700;
  display: flex;
  text-align: center;
  align-items: flex-start;
}
.arrow-right {
  width: 0;
  height: 0;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
  border-left: 15px solid #14d1f2;
}
.arrow-box {
  width: 22px;
  height: 30px;
  margin: 0 0 19px 20px;
}
</style>
