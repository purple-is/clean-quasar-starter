<template>
  <q-page class="bg-white">
    <q-tabs v-model="tab">
      <q-tab name="local" label="local" />
      <q-tab name="remote" label="remote" />
      <q-tab name="HTTP" label="HTTP" />
    </q-tabs>
    <div class="flex flex-center">
      <q-tab-panels v-model="tab" animated class="flex flex-center">
        <q-tab-panel class="q-pa-none" name="remote">
          <ChromeCastURL></ChromeCastURL>
        </q-tab-panel>

        <q-tab-panel class="q-pa-none" name="local">
          <ChromeCastLocal></ChromeCastLocal>
        </q-tab-panel>

        <q-tab-panel class="q-pa-none" name="HTTP">
          <httpd-video />
        </q-tab-panel>
      </q-tab-panels>
    </div>
  </q-page>
</template>

<script>
import ChromeCastURL from "src/components/ChromeCastURL.vue";
import ChromeCastLocal from "src/components/ChromeCastLocal.vue";
import HttpdVideo from "src/components/HttpdVideo.vue";
import videojs from "video.js";
import chromecast from "@silvermine/videojs-chromecast";
import "video.js/dist/video-js.css";

export default {
  components: { ChromeCastURL, ChromeCastLocal, HttpdVideo },
  name: "PageIndex",
  data() {
    return {
      tab: "local",
    };
  },
  created() {
    chromecast(videojs);
  }
};
</script>
