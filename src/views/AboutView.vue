<template>
  <div id="LINE" class="container">
    <h1>{{ title }}</h1>
    <div class="row">
      <div class="col">
        <input type="text" v-model="tag" />
      </div>
      <div class="row g-0 gy-2">
        <div class="col">
          <button
            type="button"
            class="btn btn-outline-info"
            @click="generateQRcodeFn()"
          >
            確定
          </button>
        </div>
      </div>
      <div>
        <canvas id="canvas"></canvas>
      </div>
      <div class="row g-0">
        <div class="col">
          <input type="text" v-model="emitText" />
        </div>
      </div>
      <div class="row g-0 gy-2">
        <div class="col">
          <button
            type="button"
            class="btn btn-outline-info"
            @click="emitNotifyFn()"
          >
            傳送通知
          </button>
        </div>
      </div>
      <h2>{{ apiStatus }}</h2>
    </div>
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
        apiStatus.value = e;
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
h1 {
  border-bottom: 1px solid rgba(0, 0, 0, 0.255);
  padding-bottom: 15px;
  margin-bottom: 25px;
}
h2 {
  border-top: 1px solid rgba(0, 0, 0, 0.255);
  margin-top: 25px;
  padding-top: 15px;
}
</style>
