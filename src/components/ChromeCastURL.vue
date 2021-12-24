<template>
  <div>
    <h3 class="text-center">Chromecast Remote</h3>
    <video
      ref="video"
      preload="auto"
      data-setup='{ "fluid": "true" }'
      class="video video-js full-width"
    ></video>
  </div>
</template>

<script>
import videojs from "video.js";

export default {
  name: "ChromeCastRemote",
  data() {
    return {
      player: null
    };
  },
  mounted() {
    this.player = videojs(this.$refs.video, {
      controls: true,
      techOrder: ["chromecast", "html5"],
      sources: [
        "https://f001.backblazeb2.com/file/purple-content/products/catalog/lsv_Santos_Portrait_Painting/media/lsv_Santos_Portrait_Painting_11.mp4"
      ]
    });
    this.player.chromecast()
    this.player.on("chromecastConnected", function() {
      console.log("connected");
    });
    this.player.on("chromecastDisconnected", function() {
      console.log("disconnected");
    });
  },
  beforeDestroy() {
    if (this.player) {
      this.player.dispose();
    }
    this.player = null;
  }
};
</script>
