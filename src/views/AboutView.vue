<template>
  <div id="LINE" class="container text-center">
    <h1>{{ title }}</h1>
    <div class="row">
      <div class="col">
        <input type="text" v-model="tag" placeholder="請輸入編號" />
      </div>
      <div class="row g-0 gy-2 justify-content-center">
        <div class="col-3">
          <!-- <button
            type="button"
            class="btn1 btn-black hover-filled-opacity"
            @click="generateQRcodeFn()"
          >
            <span>確定</span>
          </button> -->
          <h3 class="hover" @click="generateQRcodeFn()">Click Me</h3>
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
/* 測試效果 */
h3 {
  /* font-family: system-ui, sans-serif; */
  border: 1px solid #42b98363;
  font-size: 28px;
  margin: 0;
  cursor: pointer;
  padding: 0.2em;
}
.hover {
  --b: 0.1em; /* the thickness of the line */
  --c: #42b983; /* the color */

  color: #0000;
  padding-block: var(--b);
  background: linear-gradient(var(--c) 50%, #000 0) 0%
      calc(100% - var(--_p, 0%)) / 100% 200%,
    linear-gradient(var(--c) 0 0) 0% var(--_p, 0%) / var(--_p, 0%) var(--b)
      no-repeat;
  -webkit-background-clip: text, padding-box;
  background-clip: text, padding-box;
  transition: 0.3s var(--_s, 0s) linear,
    background-size 0.3s calc(0.3s - var(--_s, 0s));
}
.hover:hover {
  --_p: 100%;
  --_s: 0.3s;
  border: 1px solid #0000;
}

:active,
:hover,
:focus {
  outline: 0 !important;
  outline-offset: 0;
}
::before,
::after {
  position: absolute;
  content: "";
}
.btn1 {
  position: relative;
  display: inline-block;
  width: auto;
  height: auto;
  background-color: transparent;
  border: none;
  cursor: pointer;
  margin: 0px 25px 15px;
  min-width: 150px;
}
.btn1 span {
  position: relative;
  display: inline-block;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 2px;
  text-transform: uppercase;
  top: 0;
  left: 0;
  width: 100%;
  padding: 15px 20px;
  transition: 0.3s;
}
.btn-black::before {
  background-color: rgb(28, 31, 30);
  transition: 0.3s ease-out;
}
.btn-black span {
  color: rgb(255, 255, 255);
  border: 1px solid rgb(28, 31, 30);
  transition: 0.2s 0.1s;
}
.btn-black span:hover {
  color: rgb(28, 31, 30);
  transition: 0.2s 0.1s;
}
/* 5. hover-filled-opacity */
.btn1.hover-filled-opacity::before {
  top: 0;
  bottom: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 1;
}
.btn1.hover-filled-opacity:hover::before {
  opacity: 0;
}

input:placeholder-shown {
}
</style>
