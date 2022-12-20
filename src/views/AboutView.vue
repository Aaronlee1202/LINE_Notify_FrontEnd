<template>
  <div id="LINE">
    <h1>{{ title }}</h1>
    <input type="text" v-model="tag" />
    <button @click="generateQRcodeFn()">確定</button>
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
  setup() {
    //reactive 只能是物件 or 陣列
    // const test = reactive();
    var oauth_URL = ref("https://3c48-118-163-94-193.ngrok.io");
    const API_url = ref("http://localhost:8000");
    const title = ref("LINE Notify");
    const emitText = ref("B1-A15 充電樁溫度過高!");
    let apiStatus = ref();
    let tag = ref("");

    const emitNotifyFn = async () => {
      apiStatus.value = "Loading ...";
      try {
        const status = await axios.get(
          `${API_url.value}/v1/emitNotify?text=${emitText.value}`
        );
        console.log("status", status);
        apiStatus.value = status.data;
      } catch (e) {
        console.log(e);
        apiStatus.value = "Error" + e;
      }
    };

    const generateQRcodeFn = () => {
      var canvas = document.getElementById("canvas");
      QRCode.toCanvas(
        canvas,
        `${oauth_URL.value}/v1/login/line_notify?tag=${tag.value}`,
        function (error) {
          if (error) console.error(error);
          console.log("QRCode success!");
        }
      );
    };

    // onMounted(() => );
    const route = useRoute();
    watch(
      () => route.params.id,
      (newId) => {
        console.log(newId);
      }
    );

    return { title, emitText, apiStatus, tag, emitNotifyFn, generateQRcodeFn };
  },
};
</script>

<style scoped>
#LINE {
  position: relative;
}
</style>
