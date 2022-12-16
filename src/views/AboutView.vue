<template>
  <div id="LINE">
    <h1>{{ title }}</h1>
    <div>
      <canvas id="canvas"></canvas>
    </div>
    <input type="text" v-model="emitText" />
    <button @click="emitNotifyFn()">傳送通知</button>
    <h2>{{ apiStatus }}</h2>
  </div>
</template>

<script>
import { ref, watch } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";
import QRCode from "qrcode";

export default {
  name: "LINE Notify",
  mounted() {
    var canvas = document.getElementById("canvas");
    QRCode.toCanvas(
      canvas,
      "https://d45f-118-163-94-193.ngrok.io/v1/login/line_notify",
      function (error) {
        if (error) console.error(error);
        console.log("QRCode success!");
      }
    );
  },
  setup() {
    //reactive 只能是物件 or 陣列
    // const test = reactive();
    const title = ref("LINE Notify");
    const emitText = ref("[FrontEnd] 充電樁異常!!!");
    let apiStatus = ref();
    const url = ref("http://localhost:8000");

    // var canvas = document.getElementById("canvas");

    const emitNotifyFn = async () => {
      apiStatus.value = "Loading ...";
      try {
        const status = await axios.get(
          `${url.value}/v1/emitNotify?text=${emitText.value}`
        );
        console.log("status", status);
        apiStatus.value = status.data;
      } catch (e) {
        console.log(e);
        apiStatus.value = "Error" + e;
      }
    };
    const route = useRoute();
    watch(
      () => route.params.id,
      (newId) => {
        console.log(newId);
      }
    );

    // onMounted(() => {
    //   QRCode.toCanvas(
    //     canvas,
    //     "https://d45f-118-163-94-193.ngrok.io/v1/login/line_notify",
    //     function (error) {
    //       if (error) console.error(error);
    //       console.log("QRCode success!");
    //     }
    //   );
    // });

    return { title, emitText, apiStatus, emitNotifyFn };
  },
};
</script>

<style scoped></style>
