<template>
  <div class="HttpdVideo">
    <h3>Load from http</h3>
    <p>Serving files at: {{ url }} </p>
    <video
      ref="video"
      preload="auto"
      data-setup='{ "fluid": "true" }'
      class="video video-js full-width"
    />
  </div>
</template>
<script>
import videojs from "video.js";
import { Platform } from "quasar";

let httpd
export default {
  data: () => ({
    url: '',
    player: null
  }),
  mounted() {
    this.player = videojs(this.$refs.video, {
      controls: true,
      techOrder: ["chromecast", "html5"],
      sources: [
        `${this.url}/videos/hs_blues11_11.mp4`
      ]
    });
    this.player.chromecast();
  },
  beforeDestroy() {
    if (this.player) {
      this.player.dispose();
    }
    this.player = null;
  },
  created() {
    if (Platform.is.capacitor) {
      const vm = this
      httpd = cordova.plugins.CorHttpd;

      httpd.startServer({
        'www_root':  `${process.env.ROOT_DIR}/public`,
        'port': 9090,
        'localhost_only': false,
      }, function(url) {
        vm.url = url
        httpd.getLocalPath((path) => {
          console.log(path)
        })
      }, function(error) {
        console.log({ error })
      })
    }
  },
  destroyed() {
    if (httpd) {
      httpd.stopServer()
    }
  }
}
</script>
